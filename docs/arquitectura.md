# Arquitectura del compilador y del intérprete

Esta guía indica dónde buscar cada responsabilidad cuando se modifica Nexis. El flujo normal del código es:

```text
fuente .nxs/.nex → lexer → parser/AST → análisis semántico → ejecución
                                                      ├─ nexisc (tree-walk)
                                                      └─ nexisi (tree-walk o bytecode/VM)
```

## Compilador

| Área | Archivo | Responsabilidad |
|---|---|---|
| Tokens | `compiler/crates/nexis_lexer/src/lib.rs` | Tipos de token, estado del lexer y recorrido de caracteres. |
| Escaneo | `compiler/crates/nexis_lexer/src/scanner.rs` | Reconoce directivas, identificadores, números, strings, interpolaciones, chars y operadores. |
| Parser general | `compiler/crates/nexis_parser/src/lib.rs` | Estado del parser, programa, declaraciones simples y asignaciones. |
| Control de flujo | `compiler/crates/nexis_parser/src/control_flow.rs` | Analiza condicionales, ciclos, `switch`, bloques y `try/catch`. |
| Declaraciones | `compiler/crates/nexis_parser/src/declarations.rs` | Funciones, structs, clases, tipos y parámetros. |
| Expresiones | `compiler/crates/nexis_parser/src/expressions.rs` | Precedencia, operadores, llamadas, acceso a miembros e índices. |
| Análisis general | `compiler/crates/nexis_sema/src/lib.rs` | Registro de unidades, tipos y funciones; coordina las fases semánticas. |
| Sentencias | `compiler/crates/nexis_sema/src/statements.rs` | Ámbitos, declaraciones, asignaciones y reglas de control de flujo. |
| Análisis de expresiones | `compiler/crates/nexis_sema/src/expressions.rs` | Tipos, operadores, llamadas, miembros y compatibilidad de argumentos. |
| Estado/entrada del runtime del compilador | `compiler/crates/nexis_codegen/src/lib.rs` | Entorno, frames, carga de programas y entrada pública del intérprete. |
| Sentencias | `compiler/crates/nexis_codegen/src/statements.rs` | Ejecución de declaraciones, asignaciones y control de flujo. |
| Expresiones | `compiler/crates/nexis_codegen/src/expressions.rs` | Evaluación de valores, llamadas, métodos y conversiones. |
| Funciones nativas y colecciones | `compiler/crates/nexis_codegen/src/builtins.rs` | Operaciones de bibliotecas nativas y colecciones integradas. |

## Intérprete y VM

| Archivo | Responsabilidad |
|---|---|
| `interpreter/crates/nexis_vm/src/evaluator.rs` | Estado y ejecución tree-walk de sentencias. |
| `interpreter/crates/nexis_vm/src/evaluator_expr.rs` | Evaluación tree-walk de expresiones y llamadas. |
| `interpreter/crates/nexis_vm/src/opcodes.rs` | Instrucciones de bytecode, estructuras de programa y formato de instrucciones. |
| `interpreter/crates/nexis_vm/src/bytecode.rs` | Traducción del AST a bytecode y desensamblado. |
| `interpreter/crates/nexis_vm/src/vm.rs` | Estado de la VM y despacho de llamadas. |
| `interpreter/crates/nexis_vm/src/run_loop.rs` | Bucle principal de ejecución y despacho de instrucciones bytecode. |
| `interpreter/crates/nexis_vm/src/vm_support.rs` | Frames, estado de bucles/excepciones y utilidades del bucle de la VM. |
| `interpreter/crates/nexis_runtime/src/` | Valores, ámbitos, errores y operaciones compartidas por los backends. |

## Cómo añadir una característica

1. Añade o ajusta los tokens en el lexer si la sintaxis introduce palabras u operadores nuevos.
2. Representa la construcción en `nexis_ast` y analiza su sintaxis en el parser.
3. Valida nombres, tipos y reglas de uso en `nexis_sema`.
4. Implementa el comportamiento en `nexis_codegen` y en tree-walk/bytecode de `nexisi`.
5. Añade un caso `.nxs` a `tests/regression/` y un ejemplo/documentación cuando sea una característica visible del lenguaje.

Procura mantener la misma semántica en los tres caminos de ejecución: compilador, intérprete tree-walk e intérprete bytecode. Las dependencias entre los archivos separados se limitan con visibilidad `pub(super)`/`pub(crate)`; no son APIs públicas del lenguaje.
