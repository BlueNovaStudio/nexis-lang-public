# Nexis Compiler (`compiler/`)

Compilador de **Nexis V0.0.1**. Toma código fuente `.nxs`, lo analiza y lo
ejecuta. El binario se llama `nexisc`.

> Regla de oro del proyecto: **el compilador y el intérprete trabajan de la
> mano**. Comparten el mismo AST, los mismos tipos y los mismos códigos de
> error, así que "mismas fallas, mismas cosas". Ver
> [el README del intérprete](../interpreter/README.md).

---

## 1. Arquitectura: el pipeline en 4 fases

```text
 fuente .nxs ──► nexis_lexer ──► nexis_parser ──► nexis_sema ──► nexis_codegen
                 (tokens)         (AST)           (tipos/errores)  (ejecución)
                  NX91             NX90           NX00..NX10
```

| Fase | Crate | Entrada → Salida | Errores NX |
|---|---|---|---|
| 1. Lexer | `crates/nexis_lexer` | fuente → `Vec<Token>` | `NX91` (string/comentario sin cerrar) |
| 2. Parser | `crates/nexis_parser` | tokens → `Program` (AST) | `NX90` (sintaxis) |
| 3. Semántica | `crates/nexis_sema` | AST → AST tipado (muta `auto`) | `NX00`–`NX10` (variables/tipos) |
| 4. Ejecución | `crates/nexis_codegen` | AST → salida por consola | `NX01` (div/0), `NX60` (formato) |

Los códigos de error y el reporter viven en `crates/nexis_errors` y los usa
cualquier fase.

## 2. El punto de entrada (`nexisc/src/main.rs`)

Es el pegamento de las fases y un buen lugar para empezar a leer:

```rust
// 1. LEXER               ── fuente   → tokens
let lexed = Lexer::new(&source).tokenize();
// 2. PARSER              ── tokens   → AST
let mut parser = Parser::new(lexed.tokens);
let mut program = parser.parse_program();
// 3. SEMÁNTICA           ── resuelve `auto` y valida
let mut sema = Sema::new();
sema.analyze(&mut program);
// 4. EJECUCIÓN           ── recorre el AST
let mut interpreter = Interpreter::new();
interpreter.run(&program);
```

Si alguna fase produce diagnósticos, se reportan con
`nexis_errors::report` (formato `error[NX..]: título` + flecha hacia la línea)
y el proceso sale con código `1`.

## 3. Estructuras clave del AST (`crates/nexis_ast`)

El AST **es el contrato** entre compilador e intérprete.

### Tipos de datos y valores

```rust
pub enum Type { Int, Float, Double, Char, String, Bool }

pub enum Value {
    Int(i64), Float(f32), Double(f64),
    Char(char), String(String), Bool(bool),
}
```

`Value` es el valor *vivo* en runtime. La VM del intérprete usa **este mismo
tipo**, de ahí que no exista conversión entre frontends.

### Expresiones

```rust
pub enum Expr {
    IntLit(i64, Span),          // 18
    Var(String, Span),          // edad
    Unary { op, operand, .. },  // -x  o  !x
    Binary { op, left, right, .. }, // a + b
    Group(Box<Expr>, Span),     // (a + b)
    InputCall(Box<ConsoleInput>, Span), // Console.input(...)
    FString(Vec<FStringPart>, Span),    // fs"...{var}..."
}
```

### Sentencias

```rust
pub enum Stmt {
    VarDecl(VarDecl),  // int a = 5 | const double PI = 3.14 | auto x = ...
    Assign(Assign),    // a = 5  |  a += 2  |  a++
    Out(ConsoleOut),   // Console.print(...) / Console.println(...)
    Input { name, name_span, input }, // Console.input(...) como sentencia
    Comment,           // comentarios y #inject (no-op)
}
```

### El Span

Cada nodo lleva su posición:

```rust
pub struct Span { pub line: usize, pub column: usize, pub length: usize }
```

Es lo que permite señalar con `^` la línea exacta en los errores.

## 4. Fases en detalle

### Lexer (`nexis_lexer`)

Un lexer manual que recorre `&str` byte a byte:

- Comentarios: `//`, `#/`, `#/*...*/#`, `#{...}#` y `#` genérico.
- Literales: `18`, `1.4f`, `135.2536`, `'A'`, `"texto"`, `fs"...{var}..."`.
- Operadores: `+ - * / % ** ++ -- += -= *= /= %= **= == != < <= > >= && || !`.
- `#inject` (módulos): tokenizado, pero **no-op** en V0.0.1.

El `f` en `1.4f` marca `Float`; un decimal sin `f` (`135.2536`) es `Double`.

### Parser (`nexis_parser`)

Parser **recursivo descendente** con precedencia clásica:

```text
or → and → eq → rel → add_sub → mul_div → pow → unary → postfix → primary
```

- `**` es asociativo a la derecha (`parse_pow` se llama a sí mismo).
- `&&`/`||` no cortocircuitan en esta versión (se evalúan ambos lados).
- Las asignaciones compuestas (`a += 1`) se traducen a
  `Assign { value: Binary(Add, Var(a), 1) }`.
- `a++` como sentencia también termina en `Assign` con `Binary(Add, ..., 1)`.

### Semántica (`nexis_sema`)

Analiza sentencia a sentencia manteniendo un entorno de `VarInfo`:

```rust
pub struct VarInfo { pub ty: Type, pub is_const: bool, pub initialized: bool }
```

- Resuelve `auto`: el tipo se toma del inicializador y **se escribe en el AST**.
- Valida tipos (`NX07`), constantes sin init (`NX06`), reasignación de
  constantes (`NX03`), variables no inicializadas (`NX00`), duplicadas
  (`NX04`) e identificadores inválidos (`NX05`).
- Detecta `a / 0` literal (`NX01`).

### Codegen/ejecución (`nexis_codegen`)

En V0.0.1 la "generación de código" es un **intérprete de árbol (tree-walk)**:
recorre `Program` y evalúa qué imprime.

Detalles que hay que conocer (y que la VM del intérprete replica):

- Una variable **sin inicializador no queda registrada** en runtime.
- `Expr::Var` de una variable inexistente devuelve `String("")` (red de
  seguridad; el sema ya habría emitido NX02/NX00).
- La coerción de `Console.input` a número falla con `NX60` y deja el valor
  por defecto (`0`, `0.0`, `false`, `'\0'`).
- Detalle: `+` concatena strings/chars/bools y promueve números al tipo
  más ancho; `/` y `%` por cero emiten `NX01`.
- `==`/`!=` y `&&`/`||` comparan **solo tipos compatibles**; si no, resultado
  `false`.

## 5. Mapa de carpetas

```text
compiler/
├── Cargo.toml          # workspace (6 crates + nexisc)
├── nexisc/             # binario: monta las fases (main.rs)
└── crates/
    ├── nexis_ast/      # AST + Type/Value (el contrato)
    ├── nexis_lexer/    # fuente → tokens
    ├── nexis_parser/   # tokens → AST
    ├── nexis_sema/     # análisis semántico
    ├── nexis_codegen/  # ejecución (tree-walk)
    └── nexis_errors/   # Span, códigos NX, reporter
```

## 6. Uso

```bash
cargo build --release --bin nexisc        # en compiler/
nexisc programa.nxs                       # ejecuta y reporta errores
nexisc --help                             # ayuda
```

## 7. Hoja de ruta hacia V1.0.0

- Emitir **bytecode real** desde `nexis_codegen` (la VM del intérprete ya
  define el ISA en `interpreter/crates/nexis_vm/src/opcodes.rs`).
- Control de flujo (`if`/`while`/`for`), funciones y módulos.
- POO: structs y clases.
- Manejo de errores: `try`/`catch`.
- Bibliotecas estándar (math, io, colecciones).