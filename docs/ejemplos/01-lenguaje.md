# Lenguaje Nexis: recorrido completo

Parte 1 del recorrido por el lenguaje (secciones 1 a 7): salida por consola,
variables, operadores, condicionales, bucles, funciones y plantillas genéricas.
La **parte 2** (variables globales, structs, clases, manejo de errores, módulos,
entrada, comentarios e integrador) continúa en
[06-lenguaje-avanzado.md](06-lenguaje-avanzado.md).

Cada bloque `nexis` es un programa independiente: puedes copiarlo a un archivo
`.nxs` y ejecutarlo con `nexisc`.

Si buscas una firma concreta, consulta la
[referencia rápida](../referencia-rapida.md).

---

## 1. Hola mundo y salida por consola

`Console.println` imprime y añade salto de línea; `Console.print` imprime sin
salto.

```nexis
Console.println("Hola, Nexis")
Console.print("Sin salto... ")
Console.print("misma línea")
Console.println("")
```

Salida:

```
Hola, Nexis
Sin salto... misma línea
```

### Concatenación e interpolación

Dos formas de mezclar texto y valores:

```nexis
string nombre = "Ana"
int edad = 20

// concatenación con +
Console.println("Hola, " + nombre + " (" + edad + ")")

// interpolación con fs"..."
Console.println(fs"Hola, {nombre} ({edad})")
Console.println(fs"El doble de {edad} es {edad * 2}")
```

Salida:

```
Hola, Ana (20)
Hola, Ana (20)
El doble de 20 es 40
```

---

## 2. Variables, constantes y tipos

Nexis es de **tipado explícito**: se escribe `tipo nombre = valor`. La única
excepción es `auto`, que deduce el tipo del inicializador.

```nexis
int entero = 42
float decimal = 3.5f
double precision = 2.7182818284
char letra = 'N'
string texto = "Nexis"
bool activo = true
auto deducido = 100

Console.println(entero)
Console.println(decimal)
Console.println(precision)
Console.println(letra)
Console.println(texto)
Console.println(activo)
Console.println(deducido)

// Las constantes no se pueden reasignar (NX03)
const int MAXIMO = 10
const string LENGUAJE = "Nexis"
Console.println(MAXIMO)
Console.println(LENGUAJE)
```

Salida:

```
42
3.5
2.7182818284
N
Nexis
true
100
10
Nexis
```

### Conversiones entre tipos

```nexis
int a = int("123")
float b = float("2.5")
double c = double("1.25")
char d = char(65)
string e = string(99)
bool f = bool("true")
bool g = bool(0)

Console.println(a + 1)
Console.println(b * 2)
Console.println(c + 0.5)
Console.println(d)
Console.println(e)
Console.println(f)
Console.println(g)
```

Salida:

```
124
5
1.75
A
99
true
false
```

---

## 3. Operadores

```nexis
int a = 7
int b = 3

Console.println("suma: " + (a + b))
Console.println("resta: " + (a - b))
Console.println("producto: " + (a * b))
Console.println("division entera: " + (a / b))
Console.println("modulo: " + (a % b))
Console.println("potencia: " + (a ** b))

Console.println("igual: " + (a == b))
Console.println("distinto: " + (a != b))
Console.println("menor: " + (a < b))
Console.println("mayor o igual: " + (a >= b))

Console.println("y: " + (a > 0 && b > 0))
Console.println("o: " + (a < 0 || b > 0))
Console.println("no: " + (!(a > 0)))
```

Salida:

```
suma: 10
resta: 4
producto: 21
division entera: 2
modulo: 1
potencia: 343
igual: false
distinto: true
menor: false
mayor o igual: true
y: true
o: true
no: false
```

### Precedencia

Los paréntesis mandan; sin ellos, `**` > `* / %` > `+ -` > comparaciones >
`&&` > `||`.

```nexis
Console.println(2 + 3 * 4)
Console.println((2 + 3) * 4)
Console.println(2 ** 3 ** 2)
Console.println(10 - 4 - 3)
Console.println(1 + 2 == 3 && 4 > 2)
```

Salida:

```
14
20
512
3
true
```

---

## 4. Condicionales

```nexis
int nota = 85

if (nota >= 90) {
    Console.println("Excelente")
} else if (nota >= 70) {
    Console.println("Bueno")
} else if (nota >= 60) {
    Console.println("Aprobado")
} else {
    Console.println("Reprobado")
}
```

Salida:

```
Bueno
```

### Condiciones anidadas y operadores lógicos

```nexis
int a = 5
int b = 5
int c = 8

if (a + b > c && a + c > b && b + c > a) {
    if (a == b && b == c) {
        Console.println("Equilátero")
    } else if (a == b || b == c || a == c) {
        Console.println("Isósceles")
    } else {
        Console.println("Escaleno")
    }
} else {
    Console.println("No es un triángulo")
}
```

Salida:

```
Isósceles
```

### `switch`

```nexis
int mes = 4
string estacion;

switch (mes) {
    case 12: case 1: case 2:
        estacion = "Verano"
        break
    case 3: case 4: case 5:
        estacion = "Otoño"
        break
    case 6: case 7: case 8:
        estacion = "Invierno"
        break
    case 9: case 10: case 11:
        estacion = "Primavera"
        break
    default:
        estacion = "Mes inválido"
}

Console.println(estacion)

char vocal = 'e'
switch (vocal) {
    case 'a': case 'e': case 'i': case 'o': case 'u':
        Console.println("Es vocal")
        break
    default:
        Console.println("No es vocal")
}
```

Salida:

```
Otoño
Es vocal
```

---

## 5. Bucles

### `while`

```nexis
int i = 0
while (i < 3) {
    Console.println("while " + i)
    i = i + 1
}
```

Salida:

```
while 0
while 1
while 2
```

### `do while` (se ejecuta al menos una vez)

```nexis
int n = 5
do {
    Console.println("do " + n)
    n = n + 1
} while (n < 3)
```

Salida:

```
do 5
```

### `for` con rangos

`..` es **inclusivo** y `...` es **exclusivo** (`a ... b` llega hasta `b - 1`).

```nexis
Console.println("inclusivo 0..3")
for i in 0 .. 3 {
    Console.println(i)
}

Console.println("exclusivo 0...3")
for i in 0...3 {
    Console.println(i)
}

Console.println("paso 2")
for i in 0 .. 10 step 2 {
    Console.println(i)
}

Console.println("descendente")
for i in 5 .. 0 step -1 {
    Console.println(i)
}
```

Salida:

```
inclusivo 0..3
0
1
2
3
exclusivo 0...3
0
1
2
paso 2
0
2
4
6
8
10
descendente
5
4
3
2
1
0
```

> Para recorrer índices usa `...`: `for i in 0 ... v.length()` nunca se pasa
> del último índice.

### `foreach` en sus cuatro formas

```nexis
#inject Vector;

Vector<string> productos = ["Arroz", "Azucar", "Aceite"]

foreach (p in productos) {
    Console.println("in: " + p)
}

foreach (p, productos) {
    Console.println("coma: " + p)
}

foreach (string p, productos) {
    Console.println("tipo: " + p)
}

foreach (char c, "Nexis") {
    Console.println("char: " + c)
}
```

Salida:

```
in: Arroz
in: Azucar
in: Aceite
coma: Arroz
coma: Azucar
coma: Aceite
tipo: Arroz
tipo: Azucar
tipo: Aceite
char: N
char: e
char: x
char: i
char: s
```

### `break` y `continue`

```nexis
for i in 1 .. 10 {
    if (i == 6) {
        break
    }
    if (i % 2 == 0) {
        continue
    }
    Console.println(i)
}
```

Salida:

```
1
3
5
```

### Bucles anidados

```nexis
for i in 1 .. 3 {
    for j in 1 .. 3 {
        Console.print(i + "x" + j + "=" + (i * j) + " ")
    }
    Console.println("")
}
```

Salida:

```
1x1=1 1x2=2 1x3=3 
2x1=2 2x2=4 2x3=6 
3x1=3 3x2=6 3x3=9 
```

---

## 6. Funciones

### Procedimiento (`void`)

```nexis
void saludar(string: nombre) {
    Console.println("Hola, " + nombre)
}

saludar("Ana")
saludar("Luis")
```

Salida:

```
Hola, Ana
Hola, Luis
```

### Función con retorno

`emit ->` devuelve el valor y termina la función.

```nexis
func suma(int: a, int: b) -> int {
    emit -> a + b
}

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

Console.println(suma(3, 5))
Console.println(clasificar(85))
```

Salida:

```
8
Bueno
```

### Retorno implícito de la última expresión

```nexis
func doble(int: x) -> int {
    x * 2
}

func es_par(int: n) -> bool {
    n % 2 == 0
}

Console.println(doble(21))
Console.println(es_par(10))
```

Salida:

```
42
true
```

### Parámetros con valor por defecto

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

Salida:

```
Hola Mundo
Hola Nexis
Hola Nexis
Hola Nexis
```

### Recursión

```nexis
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

Console.println(factorial(6))
Console.println(fib(10))
```

Salida:

```
720
55
```

### Composición de funciones

```nexis
func cuadrado(int: x) -> int {
    emit -> x * x
}

func suma_cuadrados(int: a, int: b) -> int {
    emit -> cuadrado(a) + cuadrado(b)
}

Console.println(suma_cuadrados(3, 4))
```

Salida:

```
25
```

---

## 7. Plantillas genéricas

`template <type_full T>` hace que una función sirva para cualquier tipo. El
tipo `T` se sustituye en cada llamada.

```nexis
#inject Vector;

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
Vector<double> reales = [1.5, 2.5]

Console.println(contiene(numeros, 2))
Console.println(contiene(nombres, "Luis"))
Console.println(contiene(reales, 9.0))
```

Salida:

```
true
true
false
```

### Plantilla que devuelve `T`

```nexis
#inject Vector;

template <type_full T>
func primero(Vector<T>: lista) -> T {
    emit -> lista[0]
}

template <type_full T>
func ultimo(Vector<T>: lista) -> T {
    emit -> lista[lista.length() - 1]
}

Vector<int> a = [10, 20, 30]
Vector<string> b = ["uno", "dos", "tres"]

Console.println(primero(a))
Console.println(ultimo(b))
```

Salida:

```
10
tres
```

### Varios parámetros de plantilla

```nexis
#inject Vector;

template <type_full T, type_full U>
void mostrar_dos(Vector<T>: a, Vector<U>: b) -> void {
    foreach (x in a) {
        Console.println("A: " + x)
    }
    foreach (y in b) {
        Console.println("B: " + y)
    }
}

mostrar_dos([1, 2], ["x"])
```

Salida:

```
A: 1
A: 2
B: x
```

---

> Las secciones 8 a 15 (globales, structs, clases, errores, módulos, entrada,
> comentarios e integrador) continúan en [06-lenguaje-avanzado.md](06-lenguaje-avanzado.md).