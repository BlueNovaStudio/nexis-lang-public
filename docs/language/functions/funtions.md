# Funciones en Nexis

## Introducción

Una **función** es un bloque de código con nombre que se puede ejecutar
(reutilizar) tantas veces como se quiera. Las funciones permiten:

- dividir un programa grande en partes pequeñas y legibles;
- evitar repetir código;
- recibir datos de entrada (**parámetros**);
- devolver un resultado (**valor de retorno**);
- modificar colecciones, structs y variables globales.

Nexis distingue dos formas de función:

| Forma | Se declara con | Devuelve valor | Usa `emit` |
|-------|----------------|----------------|------------|
| **Procedimiento** (sin retorno) | `void` | No | No |
| **Función con retorno** | `func ... -> tipo` | Sí | Sí |

Además, cualquier función puede ser **genérica** mediante
`template <type_full T>`, de modo que un mismo código sirva para
`Vector<int>`, `Vector<string>`, `Vector<Producto>`, etc.

---

## 1. Sintaxis general

```
template <type_full T>          // opcional, solo funciones genéricas
void nombre(parámetros) {       // procedimiento: no devuelve nada
    // cuerpo
}

template <type_full T>          // opcional
func nombre(parámetros) -> tipo {   // función con retorno
    // cuerpo
    emit -> valor               // devuelve y termina la función
}
```

### Reglas de la declaración

1. La palabra clave es `func` para funciones con retorno y `void` para
   procedimientos.
2. Cada parámetro se escribe **`tipo: nombre`** (el tipo va primero).
3. Los parámetros se separan con comas.
4. El tipo de retorno se declara después de `->`.
5. El cuerpo va entre llaves `{ }`.
6. Una función con retorno debe devolver un valor en **todas** sus rutas
   de ejecución (si no, se produce `NX30`).
7. El nombre debe ser un identificador válido: letras, números y `_`,
   sin empezar por número y sin tildes ni espacios.

---

## 2. Funciones sin retorno (`void`)

Un procedimiento ejecuta acciones (imprimir, modificar una colección,
guardar un archivo) pero no entrega un valor.

```
void saludar(string: nombre) {
    Console.println("Hola, " + nombre)
}

saludar("Ana")
// Salida: Hola, Ana
```

### Ejemplo: varias operaciones

```
void mostrar_info(string: nombre, int: edad) {
    Console.println("Nombre: " + nombre)
    Console.println("Edad: " + edad)

    if (edad >= 18) {
        Console.println("Es mayor de edad")
    } else {
        Console.println("Es menor de edad")
    }
}

mostrar_info("Ana", 20)
```

**Salida:**

```
Nombre: Ana
Edad: 20
Es mayor de edad
```

### Reglas de los procedimientos

- No llevan `-> tipo`.
- No pueden usar `emit` (error `NX36`).
- Su resultado no se puede asignar: `int x = saludar("Ana")` es inválido.
- Se llaman como una sentencia: `saludar("Ana")`.

---

## 3. Funciones con retorno

Una función con retorno calcula un valor y lo entrega con `emit ->`.

```
func suma(int: a, int: b) -> int {
    emit -> a + b
}

int resultado = suma(3, 5)
Console.println(resultado)   // 8
```

### Múltiples `emit` (rutas de salida)

`emit` termina la función inmediatamente. Es habitual tener varios:

```
func clasificar(int: nota) -> string {
    if (nota >= 90) {
        emit -> "Excelente"
    } else if (nota >= 70) {
        emit -> "Bueno"
    } else if (nota >= 60) {
        emit -> "Aprobado"
    }
    emit -> "Reprobado"
}
```

### Retorno implícito de la última expresión

En Nexis también se puede escribir la última expresión sin `emit`:

```
func doble(int: x) -> int {
    x * 2
}
```

Por claridad se recomienda usar `emit ->` de forma explícita, sobre todo
cuando hay varias ramas.

### Errores de retorno

| Situación | Código |
|-----------|--------|
| Falta una ruta de retorno | `NX30` |
| `emit` dentro de una función `void` | `NX36` |
| Tipo devuelto incompatible con el declarado | `NX07` / `NX10` |
| Asignar el resultado de un `void` | `NX07` |

---

## 4. Parámetros

### 4.1 Formato

```
func potencia(int: base, int: exponente) -> int {
    emit -> base ** exponente
}
```

- `int` es el **tipo** y `base` el **nombre**.
- Todos los parámetros son obligatorios salvo que tengan valor por defecto.
- Los argumentos se pasan **en orden posicional**.

### 4.2 Parámetros con valor por defecto

```
func saludar(string: nombre = "Mundo", int: veces = 1) -> void {
    for i in 0 ... veces {
        Console.println("Hola " + nombre)
    }
}

saludar()                    // Hola Mundo
saludar("Nexis")             // Hola Nexis
saludar("Nexis", 3)          // Hola Nexis (3 veces)
```

Reglas:

- Los parámetros con defecto van **después** de los obligatorios.
- Se puede omitir cualquier sufijo de la lista, pero no un parámetro
  intermedio.
- El valor por defecto puede ser un literal o una expresión evaluada en
  el momento de la llamada.

### 4.3 Paso de valores y de colecciones

| Tipo de argumento | Comportamiento |
|-------------------|----------------|
| `int`, `float`, `double`, `char`, `bool`, `string` | Se pasa **por valor** (una copia). La función no cambia la variable original. |
| `Vector`, `LinkedList`, `Stack`, `Queue`, `Set`, `Map`, `Tree`, `Trie`, `Graph` | Se pasa con **copia de salida**: la función puede modificarlo y los cambios se devuelven al llamador. |
| `struct` / `class` | Igual que las colecciones: los cambios de campos se devuelven al llamador. |

```
#inject Vector;

void ordenar(Vector<int>: v) -> void {
    int n = v.length()
    for i in 0 ... n {
        for j in 0 ... (n - i - 1) {
            if (v[j] > v[j + 1]) {
                int aux = v[j]
                v[j] = v[j + 1]
                v[j + 1] = aux
            }
        }
    }
}

Vector<int> numeros = [64, 34, 25, 12, 22, 11, 90]
ordenar(numeros)
Console.println(numeros)
// [11, 12, 22, 25, 34, 64, 90]
```

Esto permite escribir funciones como `ordenar`, `agregar`, `buscar`,
`invertir` o `vaciar` que actúan sobre la colección original, igual que
en Java, C# o Python.

> **Nota:** la copia de salida se aplica cuando el argumento es una
> variable. Si se pasa una expresión (`ordenar([3, 1, 2])`), el resultado
> se descarta, porque no hay variable a la que devolverlo.

### 4.4 Funciones que reciben structs

```
struct Producto {
    string nombre;
    int precio;
}

void subir_precio(Producto: p, int: cantidad) -> void {
    p.precio = p.precio + cantidad
}

Producto arroz = Producto("Arroz", 1500)
subir_precio(arroz, 200)
Console.println(arroz.precio)   // 1700
```

---

## 5. Funciones genéricas (`template`)

Una plantilla permite que la función **absorba cualquier tipo**. El
parámetro `T` se sustituye por el tipo real en cada llamada.

```
template <type_full T>
func contiene(Vector<T>: lista, T: objetivo) -> bool {
    foreach (item in lista) {
        if (item == objetivo) {
            emit -> true
        }
    }
    emit -> false
}

Vector<int> numeros = [1, 2, 3]
Vector<string> nombres = ["Ana", "Luis"]

Console.println(contiene(numeros, 2))        // true
Console.println(contiene(nombres, "Luis"))   // true
```

### Varios parámetros de plantilla

```
template <type_full T, type_full U>
func combinar(Vector<T>: a, Vector<U>: b) -> void {
    foreach (x in a) {
        Console.println(x)
    }
    foreach (y in b) {
        Console.println(y)
    }
}
```

### Plantilla que devuelve `T`

```
template <type_full T>
func primero(Vector<T>: lista) -> T {
    emit -> lista[0]
}
```

### Plantilla para ordenar cualquier colección

```
template <type_full T>
func ordenar(Vector<T>: lista) -> void {
    int n = lista.length()
    for i in 0 ... n {
        for j in 0 ... (n - i - 1) {
            if (lista[j] > lista[j + 1]) {
                T aux = lista[j]
                lista[j] = lista[j + 1]
                lista[j + 1] = aux
            }
        }
    }
}
```

Reglas de las plantillas:

- `template` va **inmediatamente antes** de `func` o `void`.
- La lista va entre `< >` y cada parámetro lleva `type_full`.
- `T` se puede usar como tipo de parámetro, de retorno y de variable local.
- No hace falta declarar `T` como struct: absorbe primitivos, structs y
  colecciones.

---

## 6. Funciones y variables globales

Una función puede **leer y modificar** variables globales (declaradas
fuera de toda función), incluidas colecciones y structs globales.

```
#inject Vector;

int contador = 0
Vector<int> historial = []

void incrementar() -> void {
    contador = contador + 1
    historial.add(contador)
}

incrementar()
incrementar()
incrementar()

Console.println(contador)    // 3
Console.println(historial)   // [1, 2, 3]
```

### Shadowing (ocultar una global)

Una variable local con el mismo nombre que una global la oculta dentro
de la función, sin modificar la global:

```
int valor = 100

func local() -> int {
    int valor = 5       // variable local, oculta la global
    emit -> valor
}

Console.println(local())    // 5
Console.println(valor)      // 100
```

### Buenas prácticas con globales

- Prefiere parámetros y valores de retorno; usa globales para estado
  realmente compartido (contadores, cachés, configuración).
- Documenta qué globales modifica cada función.
- Evita modificar una global desde muchas funciones distintas.

---

## 7. Recursión

Una función puede llamarse a sí misma. Necesita siempre un **caso base**
que corte la recursión.

```
func factorial(int: n) -> int {
    if (n <= 1) {
        emit -> 1
    }
    emit -> n * factorial(n - 1)
}

func fib(int: n) -> int {
    if (n <= 1) {
        emit -> n
    }
    emit -> fib(n - 1) + fib(n - 2)
}

Console.println(factorial(6))   // 720
Console.println(fib(10))        // 55
```

### Recursión mutua

```
func es_par(int: n) -> bool {
    if (n == 0) {
        emit -> true
    }
    emit -> es_impar(n - 1)
}

func es_impar(int: n) -> bool {
    if (n == 0) {
        emit -> false
    }
    emit -> es_par(n - 1)
}
```

Cada llamada crea su propio marco de variables: los parámetros y locales
de una llamada **no pisan** los de otra. Esto es lo que permite que la
recursión funcione correctamente.

> Una recursión sin caso base termina en `NX92` (recursión infinita).

---

## 8. Funciones que devuelven colecciones

```
#inject Vector;

func rango(int: desde, int: hasta) -> Vector<int> {
    Vector<int> salida = []
    for i in desde ... hasta + 1 {
        salida.add(i)
    }
    emit -> salida
}

func doblar(Vector<int>: lista) -> Vector<int> {
    Vector<int> salida = []
    foreach (v, lista) {
        salida.add(v * 2)
    }
    emit -> salida
}

Vector<int> numeros = rango(1, 5)
Console.println(numeros)          // [1, 2, 3, 4, 5]
Console.println(doblar(numeros))  // [2, 4, 6, 8, 10]
```

---

## 9. Funciones y métodos de clases

Dentro de un `class`, las funciones se llaman **métodos**. Tienen acceso
implícito a `self` y a los campos de la clase.

```
class Cuenta {
    float saldo = 0
    int operaciones = 0

    init(self, float: inicial) {
        self.saldo = inicial
    }

    void depositar(float: monto) {
        saldo = saldo + monto
        operaciones = operaciones + 1
    }

    func retirar(float: monto) -> bool {
        if (monto > saldo) {
            emit -> false
        }
        saldo = saldo - monto
        operaciones = operaciones + 1
        emit -> true
    }

    func resumen() -> string {
        emit -> "saldo=" + saldo + " ops=" + operaciones
    }
}

Cuenta c = Cuenta(100.0)
c.depositar(50.0)
bool ok = c.retirar(30.0)
Console.println(ok)            // true
Console.println(c.resumen())   // saldo=120 ops=2
```

Reglas de los métodos:

- `init` es el constructor y puede llevar parámetros.
- `self` está disponible siempre; se puede declarar de forma explícita
  en `init(self, ...)` o usar directamente.
- Los campos se leen y escriben sin `self.` (aunque `self.campo` también
  es válido y más explícito).
- Un método se llama con `objeto.metodo(argumentos)`.

---

## 10. Llamadas y composición

Una función puede llamar a otras, y el resultado de una puede ser
argumento de otra:

```
func cuadrado(int: x) -> int {
    emit -> x * x
}

func suma_cuadrados(int: a, int: b) -> int {
    emit -> cuadrado(a) + cuadrado(b)
}

Console.println(suma_cuadrados(3, 4))   // 25
```

También se puede llamar dentro de un bucle o condición:

```
for i in 1 .. 5 {
    if (es_par(i)) {
        Console.println(i)
    }
}
```

---

## 11. Errores comunes

### Error 1: Asignar el resultado de un `void`

```
int r = mostrar_suma(5, 3)   // error
```

**Solución:** llamar como sentencia.

```
mostrar_suma(5, 3)
```

### Error 2: Usar `emit` en un `void`

```
void mostrar(int: x) {
    emit -> x    // NX36
}
```

**Solución:** usar `func ... -> int` o eliminar el `emit`.

### Error 3: Olvidar una ruta de retorno

```
func signo(int: x) -> int {
    if (x > 0) {
        emit -> 1
    }
    // falta el caso x <= 0 → NX30
}
```

**Solución:** cubrir todas las ramas con un `emit` final.

### Error 4: Número incorrecto de argumentos

```
func suma(int: a, int: b) -> int { emit -> a + b }
suma(1)          // NX32: faltan argumentos
suma(1, 2, 3)    // NX32: sobran argumentos
```

### Error 5: Tipo de argumento incompatible

```
suma("hola", 2)   // NX07/NX10
```

### Error 6: Declarar dos funciones con el mismo nombre y firma

```
func f(int: x) -> int { emit -> x }
func f(int: y) -> int { emit -> y }   // NX34
```

### Error 7: Recursión sin caso base

```
func f(int: n) -> int {
    emit -> f(n + 1)   // NX92
}
```

---

## 12. Buenas prácticas

1. **Un nombre descriptivo por acción**: `calcular_promedio`,
   `buscar_producto`, `guardar_reporte`.
2. **Pocos parámetros**: si una función necesita más de 4 o 5, agrupa
   datos en un `struct`.
3. **Una responsabilidad por función**: calcula *o* imprime, no ambas.
4. **Devuelve valores en vez de imprimir** cuando el resultado se vaya a
   reutilizar.
5. **Usa `void` explícito** en procedimientos, aunque el lenguaje permita
   omitirlo.
6. **Documenta los efectos secundarios**: qué globales o colecciones
   modifica.
7. **Prefiere plantillas** antes que duplicar la misma función para cada
   tipo.
8. **Usa `...` para recorrer índices** (`for i in 0 ... lista.length()`)
   y `..` cuando quieras incluir el límite.
9. **Cubre todas las rutas** de una función con retorno.
10. **Prueba los casos límite**: cero, negativos, colecciones vacías y
    valores repetidos.

---

## 13. Ejemplo integrador

```
#inject Vector;

struct Producto {
    string nombre;
    int precio;
}

Vector<Producto> inventario = []

void agregar(Producto: p) -> void {
    inventario.add(p)
}

template <type_full T>
func contiene(Vector<T>: lista, T: objetivo) -> bool {
    foreach (item in lista) {
        if (item == objetivo) {
            emit -> true
        }
    }
    emit -> false
}

func total() -> int {
    int suma = 0
    foreach (Producto p, inventario) {
        suma = suma + p.precio
    }
    emit -> suma
}

func mas_caro() -> Producto {
    Producto mejor = inventario[0]
    foreach (Producto p, inventario) {
        if (p.precio > mejor.precio) {
            mejor = p
        }
    }
    emit -> mejor
}

agregar(Producto("Arroz", 1500))
agregar(Producto("Leche", 3200))
agregar(Producto("Pan", 800))

Console.println("Total: " + total())
Console.println("Más caro: " + mas_caro().nombre)
Console.println("Productos: " + inventario.length())
```

Con esto quedan cubiertos: procedimientos, funciones con retorno,
parámetros por defecto, plantillas, colecciones mutables, structs,
globales, recursión y métodos de clase.
