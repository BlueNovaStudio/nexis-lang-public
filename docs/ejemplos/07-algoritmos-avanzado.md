# 🧮 Algoritmos avanzados en Nexis

Continuación de [04-algoritmos.md](04-algoritmos.md): recursión, matrices,
cadenas, matemáticas y un programa integrador (ranking de palabras).

---

## 3. Recursión

### 3.1 Factorial y Fibonacci

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
Console.println(factorial(0))
Console.println(fib(10))
Console.println(fib(15))
```

Salida:

```
720
1
55
610
```

> `fib` recursivo es exponencial. Para valores grandes usa iteración o
> memoización con un `Vector`.

### 3.2 Suma de dígitos y potencia rápida

```nexis
func suma_digitos(int: n) -> int {
    if (n < 10) {
        emit -> n
    }
    emit -> (n % 10) + suma_digitos(n / 10)
}

func potencia_rapida(int: base, int: exp) -> int {
    if (exp == 0) {
        emit -> 1
    }
    if (exp % 2 == 0) {
        int mitad = potencia_rapida(base, exp / 2)
        emit -> mitad * mitad
    }
    emit -> base * potencia_rapida(base, exp - 1)
}

Console.println(suma_digitos(9875))
Console.println(potencia_rapida(2, 10))
Console.println(potencia_rapida(3, 5))
```

Salida:

```
29
1024
243
```

### 3.3 Torres de Hanoi

Mueve `n` discos de `origen` a `destino` usando `auxiliar`. Genera
`2^n - 1` movimientos.

```nexis
void hanoi(int: n, string: origen, string: destino, string: auxiliar) -> void {
    if (n == 1) {
        Console.println(origen + " -> " + destino)
    } else {
        hanoi(n - 1, origen, auxiliar, destino)
        Console.println(origen + " -> " + destino)
        hanoi(n - 1, auxiliar, destino, origen)
    }
}

hanoi(3, "A", "C", "B")
```

Salida:

```
A -> C
A -> B
C -> B
A -> C
B -> A
B -> C
A -> C
```

### 3.4 Recursión sobre una colección

```nexis
#inject Vector;

func suma_vector(Vector<int>: v, int: indice) -> int {
    if (indice >= v.length()) {
        emit -> 0
    }
    emit -> v[indice] + suma_vector(v, indice + 1)
}

func maximo_vector(Vector<int>: v, int: indice) -> int {
    if (indice == v.length() - 1) {
        emit -> v[indice]
    }
    int resto = maximo_vector(v, indice + 1)
    if (v[indice] > resto) {
        emit -> v[indice]
    }
    emit -> resto
}

Vector<int> datos = [3, 9, 2, 7, 5]
Console.println(suma_vector(datos, 0))
Console.println(maximo_vector(datos, 0))
```

Salida:

```
26
9
```

---

## 4. Matrices

Una matriz es un `Vector<Vector<int>>`. Se recorre con dos bucles.

### 4.1 Recorrido y suma de filas

```nexis
#inject Vector;

Vector<Vector<int>> m = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

for i in 0 ... m.length() {
    int suma = 0
    for j in 0 ... m[i].length() {
        suma = suma + m[i][j]
    }
    Console.println(fs"fila {i}: {suma}")
}

Console.println(m[1][2])
Console.println(m.length())
Console.println(m[0].length())
```

Salida:

```
fila 0: 6
fila 1: 15
fila 2: 24
6
3
3
```

### 4.2 Transpuesta

```nexis
#inject Vector;

Vector<Vector<int>> m = [
    [1, 2, 3],
    [4, 5, 6]
]

Vector<Vector<int>> t = []
for j in 0 ... m[0].length() {
    Vector<int> fila = []
    for i in 0 ... m.length() {
        fila.add(m[i][j])
    }
    t.add(fila)
}

Console.println(t)
```

Salida:

```
[[1, 4], [2, 5], [3, 6]]
```

### 4.3 Multiplicación de matrices

`A` (n×m) por `B` (m×p) da `C` (n×p). El bucle interno recorre la dimensión
compartida.

```nexis
#inject Vector;

Vector<Vector<int>> a = [
    [1, 2],
    [3, 4]
]
Vector<Vector<int>> b = [
    [5, 6],
    [7, 8]
]

Vector<Vector<int>> c = []
for i in 0 ... a.length() {
    Vector<int> fila = []
    for j in 0 ... b[0].length() {
        int suma = 0
        for k in 0 ... b.length() {
            suma = suma + a[i][k] * b[k][j]
        }
        fila.add(suma)
    }
    c.add(fila)
}

Console.println(c)
Console.println(c[0][0])
Console.println(c[1][1])
```

Salida:

```
[[19, 22], [43, 50]]
19
50
```

### 4.4 Matriz identidad y diagonal

```nexis
#inject Vector;

int n = 3
Vector<Vector<int>> identidad = []

for i in 0 ... n {
    Vector<int> fila = []
    for j in 0 ... n {
        if (i == j) {
            fila.add(1)
        } else {
            fila.add(0)
        }
    }
    identidad.add(fila)
}

Console.println(identidad)

int traza = 0
for i in 0 ... n {
    traza = traza + identidad[i][i]
}
Console.println(traza)
```

Salida:

```
[[1, 0, 0], [0, 1, 0], [0, 0, 1]]
3
```

---

## 5. Cadenas

### 5.1 Palíndromo

Ignora espacios y compara desde los extremos.

```nexis
#inject string;

func es_palindromo(string: texto) -> bool {
    string limpio = ""
    foreach (char c, texto) {
        if (c != ' ') {
            limpio = limpio + c
        }
    }

    int n = string.length(limpio)
    for i in 0 ... n / 2 {
        if (limpio[i] != limpio[n - 1 - i]) {
            emit -> false
        }
    }
    emit -> true
}

Console.println(es_palindromo("anita lava la tina"))
Console.println(es_palindromo("reconocer"))
Console.println(es_palindromo("nexis"))
```

Salida:

```
true
true
false
```

### 5.2 Contar vocales

```nexis
#inject string;

func contar_vocales(string: texto) -> int {
    int total = 0
    foreach (char c, texto) {
        if (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u') {
            total = total + 1
        }
    }
    emit -> total
}

Console.println(contar_vocales("programacion"))
Console.println(contar_vocales("NEXIS"))
```

Salida:

```
5
0
```

> Las mayúsculas no cuentan. Normaliza con `string.lowercase(texto)` antes de
> llamar si las necesitas.

### 5.3 Invertir una cadena

```nexis
#inject string;

func invertir(string: texto) -> string {
    string resultado = ""
    for i in 0 ... string.length(texto) {
        resultado = resultado + texto[string.length(texto) - 1 - i]
    }
    emit -> resultado
}

Console.println(invertir("Nexis"))
Console.println(invertir("12345"))
```

Salida:

```
sixeN
54321
```

### 5.4 Anagramas

Dos palabras son anagramas si tienen las mismas letras. Se ordenan sus
caracteres y se comparan.

```nexis
#inject string;
#inject Vector;

func normalizar(string: texto) -> string {
    Vector<string> letras = string.split(string.lowercase(texto), "")
    letras.sort()
    string resultado = ""
    foreach (l in letras) {
        resultado = resultado + l
    }
    emit -> resultado
}

func son_anagramas(string: a, string: b) -> bool {
    emit -> normalizar(a) == normalizar(b)
}

Console.println(son_anagramas("roma", "amor"))
Console.println(son_anagramas("Nexis", "sixen"))
Console.println(son_anagramas("hola", "mundo"))
```

Salida:

```
true
true
false
```

### 5.5 Frecuencia de caracteres

```nexis
#inject string;
#inject Map;
#inject Vector;

Map<string, int> frecuencia = {}
foreach (char c, "banana") {
    string clave = c
    if (frecuencia.contains(clave)) {
        frecuencia.put(clave, frecuencia.get(clave) + 1)
    } else {
        frecuencia.put(clave, 1)
    }
}

Vector<string> claves = frecuencia.keys()
claves.sort()
foreach (k in claves) {
    Console.println(k + ": " + frecuencia.get(k))
}
```

Salida:

```
a: 3
b: 1
n: 2
```

---

## 6. Matemáticas

### 6.1 Máximo común divisor y mínimo común múltiplo

Algoritmo de Euclides.

```nexis
func gcd(int: a, int: b) -> int {
    while (b != 0) {
        int temp = b
        b = a % b
        a = temp
    }
    emit -> a
}

func lcm(int: a, int: b) -> int {
    emit -> (a / gcd(a, b)) * b
}

Console.println(gcd(48, 18))
Console.println(gcd(17, 5))
Console.println(lcm(4, 6))
Console.println(lcm(21, 6))
```

Salida:

```
6
1
12
42
```

### 6.2 ¿Es primo?

```nexis
#inject math;

func es_primo(int: n) -> bool {
    if (n < 2) {
        emit -> false
    }
    if (n == 2) {
        emit -> true
    }
    if (n % 2 == 0) {
        emit -> false
    }
    int limite = int(math.sqrt(n))
    for i in 3 .. limite step 2 {
        if (n % i == 0) {
            emit -> false
        }
    }
    emit -> true
}

Console.println(es_primo(2))
Console.println(es_primo(17))
Console.println(es_primo(18))
Console.println(es_primo(1))
Console.println(es_primo(97))
```

Salida:

```
true
true
false
false
true
```

### 6.3 Criba de Eratóstenes

Encuentra todos los primos hasta `n` marcando múltiplos.

```nexis
#inject Vector;

func primos_hasta(int: n) -> Vector<int> {
    Vector<bool> es_primo = []
    for i in 0 .. n {
        es_primo.add(true)
    }
    es_primo[0] = false
    if (n >= 1) {
        es_primo[1] = false
    }

    for i in 2 .. n {
        if (es_primo[i]) {
            int multiplo = i * i
            while (multiplo <= n) {
                es_primo[multiplo] = false
                multiplo = multiplo + i
            }
        }
    }

    Vector<int> resultado = []
    for i in 0 .. n {
        if (es_primo[i]) {
            resultado.add(i)
        }
    }
    emit -> resultado
}

Console.println(primos_hasta(30))
Console.println(primos_hasta(10).length())
```

Salida:

```
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29]
4
```

### 6.4 Suma de una serie

```nexis
#inject math;

double armonica = 0.0
for i in 1 .. 10 {
    armonica = armonica + 1.0 / double(i)
}
Console.println(math.round(armonica * 1000.0) / 1000.0)

int suma_cuadrados = 0
for i in 1 .. 10 {
    suma_cuadrados = suma_cuadrados + i * i
}
Console.println(suma_cuadrados)
```

Salida:

```
2.929
385
```

---

## 7. Programa integrador: ranking de palabras

Combina `Map` para contar, `Vector` para ordenar y funciones para separar
responsabilidades. El desempate es alfabético para que la salida sea estable.

```nexis
#inject Map;
#inject Vector;
#inject string;

func contar(string: texto) -> Map<string, int> {
    Map<string, int> frecuencia = {}
    Vector<string> palabras = string.split(string.lowercase(texto), " ")
    foreach (p in palabras) {
        if (string.length(p) > 0) {
            if (frecuencia.contains(p)) {
                frecuencia.put(p, frecuencia.get(p) + 1)
            } else {
                frecuencia.put(p, 1)
            }
        }
    }
    emit -> frecuencia
}

func ordenar_por_frecuencia(Map<string, int>: frecuencia) -> Vector<string> {
    Vector<string> claves = frecuencia.keys()

    // seleccion: mas frecuente primero; empate -> alfabetico
    for i in 0 ... claves.length() - 1 {
        int mejor = i
        for j in i + 1 ... claves.length() {
            int fj = frecuencia.get(claves[j])
            int fm = frecuencia.get(claves[mejor])
            if (fj > fm || (fj == fm && claves[j] < claves[mejor])) {
                mejor = j
            }
        }
        if (mejor != i) {
            string tmp = claves[i]
            claves[i] = claves[mejor]
            claves[mejor] = tmp
        }
    }

    emit -> claves
}

string texto = "el gato y el perro y el gato y el raton"
Map<string, int> frecuencia = contar(texto)
Vector<string> ranking = ordenar_por_frecuencia(frecuencia)

Console.println("palabras distintas: " + ranking.length())
for i in 0 ... 4 {
    Console.println((i + 1) + ". " + ranking[i] + " (" + frecuencia.get(ranking[i]) + ")")
}

Console.println("total 'el': " + frecuencia.get("el"))
Console.println("existe 'perro': " + frecuencia.contains("perro"))
Console.println("existe 'leon': " + frecuencia.contains("leon"))
```

Salida:

```
palabras distintas: 5
1. el (4)
2. y (3)
3. gato (2)
4. perro (1)
total 'el': 4
existe 'perro': true
existe 'leon': false
```

### ¿Qué se practicó?

| Concepto | Dónde aparece |
|----------|---------------|
| `Map` | conteo de frecuencias |
| `Vector` | claves, ranking, recorridos |
| `string` | `split`, `lowercase`, `length` |
| Funciones | `contar`, `ordenar_por_frecuencia` |
| Paso por copia de salida | el `Map` y el `Vector` se devuelven y modifican |
| Ordenamiento manual | selección con desempate |
| Bucles anidados | comparación de pares |
| Condiciones compuestas | `fj > fm || (fj == fm && ...)` |