# ⚡ Referencia rápida de Nexis V0.0.6

Parte 1 (sintaxis del lenguaje, secciones 1 a 14). La **parte 2** —API de
colecciones, API de librerías, errores y ejemplos— está en
[referencia-api.md](referencia-api.md).

Para ejemplos ejecutables, consulta los
[capítulos de ejemplos](ejemplos/01-lenguaje.md).

---

## 1. Estructura de un programa

Un programa es una secuencia de sentencias. No hay función `main`: el código
de nivel superior se ejecuta de arriba a abajo.

```nexis
#inject Vector;

int total = 0
foreach (n in [1, 2, 3]) {
    total = total + n
}
Console.println(total)
```

Salida:

```
6
```

---

## 2. Comentarios

```nexis
# comentario de línea (estilo numeral)
// comentario de línea (estilo barras)

/*
   comentario
   de bloque
*/

Console.println("ok")   // comentario al final de la línea
```

Salida:

```
ok
```

---

## 3. Tipos primitivos

| Tipo | Ejemplo | Notas |
|------|---------|-------|
| `int` | `42` | Entero con signo. |
| `short` | `7` | Entero corto. |
| `long` | `1000000` | Entero largo. |
| `unsigned` | `10` | Entero sin signo. |
| `float` | `3.5` | Coma flotante. |
| `double` | `2.7182818284` | Doble precisión. |
| `char` | `'A'` | Un carácter entre comillas simples. |
| `string` | `"Nexis"` | Cadena entre comillas dobles. |
| `bool` | `true`, `false` | Booleano. |
| `void` | — | Sin valor (solo retorno de funciones). |
| `auto` | `auto x = 10` | Deduce el tipo del inicializador. |

---

## 4. Variables y constantes

```nexis
int entero = 42
double real = 2.5
string texto = "Nexis"
bool activo = true
auto deducido = 100          // int

const int MAXIMO = 10
const string NOMBRE = "Nexis"

entero = 50                  // permitido
// MAXIMO = 20               // NX03: constante
```

Reglas:

- La declaración siempre lleva tipo (salvo `auto`, que exige inicializador).
- No existe `:=` ni `+=`; usa `x = x + 1`.
- Una variable no puede redeclararse en el mismo ámbito (`NX04`).

---

## 5. Operadores

### Aritméticos

| Operador | Descripción | Ejemplo |
|----------|-------------|---------|
| `+` | suma / concatenación | `2 + 3`, `"a" + "b"` |
| `-` | resta | `7 - 3` |
| `*` | multiplicación | `4 * 5` |
| `/` | división (entera si ambos son enteros) | `7 / 2` → `3` |
| `%` | módulo | `7 % 3` → `1` |
| `**` | potencia | `2 ** 10` → `1024` |

### Comparación

`==`, `!=`, `<`, `>`, `<=`, `>=` devuelven `bool`.

### Lógicos

`&&` (y), `||` (o), `!` (no).

### Precedencia (de mayor a menor)

1. `()`
2. `**`
3. `*`, `/`, `%`
4. `+`, `-`
5. `<`, `<=`, `>`, `>=`
6. `==`, `!=`
7. `&&`
8. `||`

```nexis
Console.println(2 + 3 * 4)
Console.println((2 + 3) * 4)
Console.println(2 ** 3 ** 2)
Console.println(true || false && false)
```

Salida:

```
14
20
512
true
```

> `**` asocia a la derecha: `2 ** 3 ** 2` es `2 ** 9`.

### Rangos

| Operador | Significado | Ejemplo |
|----------|-------------|---------|
| `a .. b` | inclusivo: llega hasta `b` | `0 .. 3` → 0, 1, 2, 3 |
| `a ... b` | exclusivo: llega hasta `b - 1` | `0 ... 3` → 0, 1, 2 |

---

## 6. Literales de colecciones

```nexis
#inject Vector;
#inject Map;
#inject Set;

Vector<int> v = [1, 2, 3]
Vector<string> s = ["a", "b"]
Vector<Vector<int>> m = [[1, 2], [3, 4]]

Map<string, int> mapa = {"a": 1, "b": 2}
Set<int> conjunto = {1, 2, 3}

Vector<int> vacio = []
Map<string, int> mapa_vacio = {}
Set<int> conjunto_vacio = {}
```

> Los literales deben ser homogéneos: `[1, "dos"]` produce `NX07`.

---

## 7. Control de flujo

### `if` / `else if` / `else`

```nexis
int n = 5
if (n > 0) {
    Console.println("positivo")
} else if (n < 0) {
    Console.println("negativo")
} else {
    Console.println("cero")
}
```

La condición debe ser `bool` (`NX23`).

### `switch`

```nexis
int opcion = 2
switch (opcion) {
    case 1:
        Console.println("uno")
        break
    case 2: case 3:
        Console.println("dos o tres")
        break
    default:
        Console.println("otro")
}
```

- `case` agrupados: `case 2: case 3:`.
- `break` es necesario para no caer al siguiente caso.
- No se permiten dos `case` con el mismo valor (`NX24`).

### `while`

```nexis
int i = 0
while (i < 3) {
    Console.println(i)
    i = i + 1
}
```

### `do while`

```nexis
int i = 10
do {
    Console.println("una vez")
    i = i + 1
} while (i < 3)
```

### `for` con rangos

```nexis
for i in 0 .. 3 {           // 0, 1, 2, 3
    Console.println(i)
}

for i in 0 ... 3 {          // 0, 1, 2
    Console.println(i)
}

for i in 0 .. 10 step 2 {   // 0, 2, 4, 6, 8, 10
    Console.println(i)
}

for i in 5 .. 0 step -1 {   // 5, 4, 3, 2, 1, 0
    Console.println(i)
}
```

> Sin `step -1`, un rango descendente no produce iteraciones.

### `foreach`

Cuatro formas válidas:

```nexis
#inject Vector;

Vector<string> lista = ["a", "b"]

foreach (x in lista) { }          // elemento
foreach (x, lista) { }            // elemento
foreach (string x, lista) { }     // elemento con tipo
foreach (char c, "Nexis") { }     // carácter de una cadena
```

### `break` y `continue`

```nexis
for i in 1 .. 10 {
    if (i == 6) { break }
    if (i % 2 == 0) { continue }
    Console.println(i)
}
```

Salida:

```
1
3
5
```

---

## 8. Funciones

### Declaración

```nexis
void saludar(string: nombre) {
    Console.println("Hola " + nombre)
}

func sumar(int: a, int: b) -> int {
    emit -> a + b
}
```

- `void nombre(params) { ... }` no devuelve valor.
- `func nombre(params) -> tipo { ... }` devuelve un valor.
- Cada parámetro se escribe `tipo: nombre`.

### Retorno

```nexis
func doble(int: x) -> int {
    emit -> x * 2          // retorno explícito
}

func triple(int: x) -> int {
    x * 3                  // retorno implícito de la última expresión
}
```

`emit` termina la función. En una función `void` no se puede usar (`NX36`).

### Parámetros por defecto

```nexis
func saludar(string: nombre = "Mundo", int: veces = 1) -> void {
    for i in 0 ... veces {
        Console.println("Hola " + nombre)
    }
}

saludar()
saludar("Nexis")
saludar("Nexis", 2)
```

### Plantillas genéricas

`template <type_full T>` permite que una función acepte cualquier tipo:

```nexis
#inject Vector;

template <type_full T>
func primero(Vector<T>: lista) -> T {
    emit -> lista[0]
}

Console.println(primero([10, 20]))
Console.println(primero(["a", "b"]))
```

Salida:

```
10
a
```

Varios parámetros de plantilla:

```nexis
template <type_full T, type_full U>
func combinar(T: a, U: b) -> string {
    emit -> string(a) + "-" + string(b)
}
```

### Paso de parámetros

| Tipo de valor | Semántica |
|---------------|-----------|
| Primitivos (`int`, `string`, `bool`, …) | Por valor: la función recibe una copia. |
| `Vector`, `Map`, `Set`, `Tree`, `Trie`, `Graph`, `LinkedList`, `Stack`, `Queue` | **Copia de salida**: los cambios vuelven al llamador. |
| `struct` | Copia de salida: los cambios de campos vuelven al llamador. |

```nexis
#inject Vector;

void ordenar(Vector<int>: v) -> void {
    v.sort()
}

Vector<int> datos = [3, 1, 2]
ordenar(datos)
Console.println(datos)   // [1, 2, 3]
```

### Variables globales

Las funciones ven y modifican las variables globales:

```nexis
int contador = 0

void incrementar() -> void {
    contador = contador + 1
}

incrementar()
incrementar()
Console.println(contador)
```

Salida:

```
2
```

---

## 9. Structs

```nexis
struct Producto {
    string nombre;
    int precio;
    int stock;
}

Producto p = Producto("Arroz", 1500, 10)
Console.println(p.nombre)

p.precio = 1700
Console.println(p.precio)
```

Reglas:

- Campos separados por `;`.
- Constructor posicional `Nombre(valor1, valor2, ...)`.
- Acceso y asignación con `.campo`.
- Un struct puede contener colecciones y otros structs.

> Para modificar el campo de un elemento indexado, copia el struct, modifica y
> reasigna:
>
> ```nexis
> #inject Vector;
> struct Producto {
>     string nombre;
>     int precio;
>     int stock;
> }
> Vector<Producto> lista = [Producto("Pan", 800, 5)]
> Producto tmp = lista[0]
> tmp.stock = 9
> lista[0] = tmp
> Console.println(lista[0].stock)
> ```
>
> Salida: `9`

---

## 10. Clases

```nexis
class Cuenta {
    float saldo = 0
    int operaciones = 0

    init(self, float: inicial) {
        self.saldo = inicial
    }

    void depositar(float: monto) {
        saldo = saldo + monto       // self implícito
        operaciones = operaciones + 1
    }

    func resumen() -> string {
        emit -> "saldo=" + saldo
    }
}

Cuenta c = Cuenta(100.0)
c.depositar(50.0)
Console.println(c.resumen())
```

Salida:

```
saldo=150
```

Reglas:

- Los campos se declaran con valor inicial.
- `init(self, ...)` es el constructor; `self` también puede escribirse `this`.
- Dentro de los métodos, los campos se usan directamente (sin `self.`).
- Una clase sin `init` se instancia con `Nombre()`.

---

## 11. Manejo de errores

```nexis
try {
    int x = 10 / 0
} catch (ErrorDivision e) {
    Console.println("división por cero")
} catch (Error e) {
    Console.println("otro error: " + e.mensaje())
} finally {
    Console.println("siempre")
}
```

### Lanzar

```nexis
func validar(int: edad) -> void {
    if (edad < 0) {
        lanzar ErrorValidacion("edad negativa")
    }
}
```

`throw` es alias de `lanzar`.

### Tipos de error

| Tipo | Códigos típicos |
|------|-----------------|
| `Error` | base de todos |
| `ErrorDivision` | NX01 |
| `ErrorIndice` | NX11 |
| `ErrorTipo` | NX07, NX10, NX12, NX33 |
| `ErrorMemoria` | NX92 |
| `ErrorArchivo` | NX61, NX62 |
| `ErrorEntrada` | NX60 |
| `ErrorValidacion` | NX12, NX60 |
| `ErrorRed` | NX70 |
| `ErrorGrafico` | NX71 |
| `ErrorAssert` | NX44 |
| `ErrorMatematico` | NX01, NX13 |

### Métodos útiles

- `e.mensaje()` → texto del error.

> No hay `e.codigo()` en V0.0.6; el código `NXxx` aparece en el mensaje
> impreso por el compilador o en la salida de error no capturado.

---

## 12. Módulos

### Librerías nativas

```nexis
#inject math;
#inject string;
#inject Vector;
```

### Archivos propios (`.nex`)

```text
# geometria.nex
#inject math;

func area_circulo(float: r) -> float {
    emit -> math.PI * r * r
}
```

```text
# main.nxs
#inject "geometria.nex";

Console.println(area_circulo(5.0))
```

- La ruta es relativa al archivo que importa.
- La extensión debe ser `.nex` (`NX83`).
- No se permiten importaciones circulares (`NX81`).

---

## 13. Consola

| Llamada | Efecto |
|---------|--------|
| `Console.print(x)` | Imprime sin salto de línea. |
| `Console.println(x)` | Imprime con salto de línea. |
| `Console.input()` | Lee una línea como `string`. |
| `Console.input("Texto: ")` | Lee mostrando un texto guía. |
| `Console.input(text="Texto: ")` | Igual, con argumento nombrado. |

`print` y `println` son **sentencias**, no expresiones.

La entrada se convierte al tipo de la variable destino:

```nexis
// doc: input 25
int edad = Console.input(text="Edad: ")
Console.println(edad + 1)
```

Salida:

```
Edad: 26
```

### Interpolación

```nexis
string nombre = "Ana"
int edad = 20
Console.println(fs"{nombre} tiene {edad} años")
Console.println(fs"doble: {edad * 2}")
```

Salida:

```
Ana tiene 20 años
doble: 40
```

> `fs"..."` no interpreta `\n`. Para saltos de línea, concatena con `"\n"`.

---

## 14. Conversiones

| Llamada | Resultado |
|---------|-----------|
| `int(x)` | Entero. |
| `float(x)` | Flotante. |
| `double(x)` | Doble precisión. |
| `char(x)` | Carácter desde código (`char(65)` → `A`) o texto de 1 carácter. |
| `string(x)` | Representación textual. |
| `bool(x)` | `bool("true")` → `true`, `bool(0)` → `false`, `bool(1)` → `true`. |

```nexis
Console.println(int("42") + 8)
Console.println(float("2.5") * 2)
Console.println(char(65))
Console.println(string(99))
Console.println(bool("false"))
```

Salida:

```
50
5
A
99
false
```

> `int("abc")` lanza `NX12` / `NX60`.

---

> La API completa de colecciones (sección 15), librerías (16), errores (17–18) y
> ejemplos (19–20) continúa en [referencia-api.md](referencia-api.md).