# 📚 Librerías estándar: math, string, file, random, time

Las librerías nativas se activan con `#inject nombre;` y se usan como
`libreria.funcion(...)`. Este capítulo tiene un ejemplo ejecutable de **cada
función implementada** en V0.0.6.

Las firmas completas están en la [referencia rápida](../referencia-rapida.md).

---

## 1. `math` — matemáticas

### Constantes

```nexis
#inject math;

Console.println(math.PI)
Console.println(math.E)
Console.println(math.PI > 3.14 && math.PI < 3.15)
```

Salida:

```
3.141592653589793
2.718281828459045
true
```

### Raíz, potencia y logaritmo

```nexis
#inject math;

Console.println(math.sqrt(81))
Console.println(math.sqrt(2.25))
Console.println(math.pow(2, 10))
Console.println(math.pow(9, 0.5))
Console.println(math.log(math.E))
Console.println(math.log(1))
```

Salida:

```
9
1.5
1024
3
1
0
```

### Valor absoluto y redondeo

```nexis
#inject math;

Console.println(math.abs(-7))
Console.println(math.abs(7))
Console.println(math.floor(3.9))
Console.println(math.ceil(3.1))
Console.println(math.round(3.5))
Console.println(math.round(3.4))
```

Salida:

```
7
7
3
4
4
3
```

### Mínimo y máximo

```nexis
#inject math;

Console.println(math.min(4, 9))
Console.println(math.max(4, 9))
Console.println(math.min(-3, -8))
Console.println(math.max(2.5, 2.4))
```

Salida:

```
4
9
-8
2.5
```

### Casos límite (no lanzan error)

```nexis
#inject math;

Console.println(math.sqrt(-1))
Console.println(math.log(0))
```

Salida:

```
NaN
-inf
```

> `NaN` e `inf` se imprimen tal cual. Compáralos con cuidado: `NaN == NaN`
> es `false`.

### Funciones reservadas

Estas están en la API planificada pero **no** están implementadas en V0.0.6;
llamarlas devuelve `void`:

`sin`, `cos`, `tan`, `asin`, `acos`, `atan`, `log10`, `log2`, `trunc`.

---

## 2. `string` — texto

### Longitud y cambio de caja

```nexis
#inject string;

string texto = "Nexis"

Console.println(string.length(texto))
Console.println(string.length(""))
Console.println(string.uppercase(texto))
Console.println(string.lowercase("HOLA"))
```

Salida:

```
5
0
NEXIS
hola
```

`string.length` cuenta **caracteres**, no bytes:

```nexis
#inject string;

Console.println(string.length("año"))
Console.println(string.length("café"))
```

Salida:

```
3
4
```

### `trim` — quitar espacios de los extremos

```nexis
#inject string;

Console.println("[" + string.trim("  hola  ") + "]")
Console.println("[" + string.trim("sin espacios") + "]")
```

Salida:

```
[hola]
[sin espacios]
```

### `split` — dividir en un `Vector<string>`

```nexis
#inject string;
#inject Vector;

Vector<string> partes = string.split("uno,dos,tres", ",")
Console.println(partes)
Console.println(partes.length())
Console.println(partes[1])

// separador vacío: devuelve un carácter por elemento
Vector<string> letras = string.split("abc", "")
Console.println(letras)
```

Salida:

```
[uno, dos, tres]
3
dos
[a, b, c]
```

> Si el texto termina en el separador, el último elemento es una cadena vacía:
> `split("a,b,", ",")` devuelve 3 elementos.

### `contains` y `startsWith`

```nexis
#inject string;

Console.println(string.contains("Nexis", "ex"))
Console.println(string.contains("Nexis", "zz"))
Console.println(string.startsWith("Nexis", "Ne"))
Console.println(string.startsWith("Nexis", "is"))
```

Salida:

```
true
false
true
false
```

### Alias en español

Cada función tiene un alias equivalente:

| Inglés | Español |
|--------|---------|
| `length` | `longitud` |
| `lowercase` | `minusculas` |
| `uppercase` | `mayusculas` |
| `trim` | `recortar` |
| `split` | `dividir` |
| `contains` | `contiene` |
| `startsWith` | `comienza_con` |

```nexis
#inject string;

Console.println(string.longitud("abc"))
Console.println(string.minusculas("ABC"))
Console.println(string.mayusculas("abc"))
Console.println(string.recortar("  x  "))
Console.println(string.dividir("a-b", "-").length())
Console.println(string.contiene("abc", "b"))
Console.println(string.comienza_con("abc", "a"))
```

Salida:

```
3
abc
ABC
x
2
true
true
```

---

## 3. `file` — archivos de texto

### `exists`, `write` y `read`

```nexis
#inject file;
#inject string;

string ruta = "doc_ejemplo.txt"

Console.println(file.exists(ruta))
file.write(ruta, "primera\nsegunda\n")
Console.println(file.exists(ruta))

string contenido = file.read(ruta)
Console.println(string.length(contenido) > 0)
Console.println(string.contains(contenido, "segunda"))
Console.println(string.split(contenido, "\n").length())
```

Salida:

```
false
true
true
true
3
```

`file.write` **sobrescribe** el archivo completo y devuelve `void`.

### Error al leer un archivo inexistente

Se lanza `ErrorArchivo` con código `NX61`:

```nexis
#inject file;

try {
    string datos = file.read("archivo_que_no_existe.txt")
    Console.println(datos)
} catch (ErrorArchivo e) {
    Console.println("ErrorArchivo capturado")
}
```

Salida:

```
ErrorArchivo capturado
```

### Procesar un archivo línea por línea

```nexis
#inject file;
#inject string;
#inject Vector;

file.write("doc_lineas.txt", "Ana,20\nLuis,25\nEva,30\n")
string contenido = file.read("doc_lineas.txt")
Vector<string> lineas = string.split(contenido, "\n")

int total = 0
foreach (linea in lineas) {
    if (linea == "") {
        continue
    }
    Vector<string> campos = string.split(linea, ",")
    total = total + int(campos[1])
}

Console.println("personas: " + (lineas.length() - 1))
Console.println("suma edades: " + total)
```

Salida:

```
personas: 3
suma edades: 75
```

> El último elemento de `split` es vacío porque el archivo acaba en `\n`; por
> eso el bucle lo salta con `continue`.

### Errores de escritura

Si la ruta no se puede escribir, se lanza `ErrorArchivo` (`NX62`):

```nexis
#inject file;

try {
    file.write("carpeta_inexistente/archivo.txt", "x")
} catch (ErrorArchivo e) {
    Console.println("No se pudo escribir")
}
```

Salida:

```
No se pudo escribir
```

---

## 4. `random` — valores pseudoaleatorios

`random.integer(min, max)` devuelve un entero en el rango **inclusivo**
`[min, max]`.

```nexis
#inject random;

int dado = random.integer(1, 6)
Console.println(dado >= 1 && dado <= 6)

int fijo = random.integer(5, 5)
Console.println(fijo)

int negativo = random.integer(-3, -1)
Console.println(negativo >= -3 && negativo <= -1)
```

Salida:

```
true
5
true
```

### Elegir un elemento al azar

```nexis
#inject random;
#inject Vector;

Vector<string> colores = ["rojo", "verde", "azul"]
int indice = random.integer(0, colores.length() - 1)

Console.println(indice >= 0 && indice < colores.length())
Console.println(colores[indice] == "rojo" || colores[indice] == "verde" || colores[indice] == "azul")
```

Salida:

```
true
true
```

> La secuencia es pseudoaleatoria y **reproducible** entre ejecuciones del
> mismo binario; no la uses para criptografía.

---

## 5. `time` — medición de tiempo

`time.clock()` devuelve los milisegundos transcurridos desde el inicio del
programa.

```nexis
#inject time;

int inicio = time.clock()
int suma = 0
for i in 0 .. 10000 {
    suma = suma + i
}
int fin = time.clock()

Console.println(suma)
Console.println(fin >= inicio)
Console.println(fin - inicio >= 0)
```

Salida:

```
50005000
true
true
```

### Medir un bloque

```nexis
#inject time;
#inject string;

int t0 = time.clock()
string acumulado = ""
for i in 0...100 {
    acumulado = acumulado + "x"
}
int t1 = time.clock()

Console.println(string.length(acumulado))
Console.println("milisegundos validos: " + (t1 - t0 >= 0))
```

Salida:

```
100
milisegundos validos: true
```

> `time.now()` y las funciones de fecha **no** están implementadas en V0.0.6.

---

## 6. Conversiones de tipo

Las conversiones son funciones globales, no métodos:

| Llamada | Resultado |
|---------|-----------|
| `int(x)` | entero |
| `float(x)` | flotante |
| `double(x)` | doble precisión |
| `char(x)` | carácter desde código o texto de 1 carácter |
| `string(x)` | representación textual |
| `bool(x)` | booleano |

```nexis
int a = int("123")
float b = float("2.5")
double c = double("1.25")
char d = char(65)
char e = char("Z")
string f = string(99)
bool g = bool("true")
bool h = bool(0)
bool i = bool(1)

Console.println(a + 1)
Console.println(b * 2)
Console.println(c + 0.5)
Console.println(d)
Console.println(e)
Console.println(f)
Console.println(g)
Console.println(h)
Console.println(i)
```

Salida:

```
124
5
1.75
A
Z
99
true
false
true
```

### Conversión desde la entrada del usuario

`Console.input()` ya devuelve el tipo de la variable destino, pero puedes
convertir explícitamente texto leído como `string`:

```nexis
// doc: input 42
string crudo = Console.input()
int numero = int(crudo)
Console.println(numero + 8)
```

Salida:

```
50
```

> `int("abc")` lanza un error de conversión (`NX12`).

---

## 7. `Console` — entrada y salida

### `print` vs `println`

```nexis
Console.print("A")
Console.print("B")
Console.println("")
Console.println("C")
Console.print(1)
Console.print(true)
Console.println("")
```

Salida:

```
AB
C
1true
```

### Interpolación `fs"..."`

```nexis
#inject string;

string nombre = "Ana"
int edad = 20

Console.println(fs"{nombre} tiene {edad} años")
Console.println(fs"El doble es {edad * 2}")
Console.println(fs"Mayúsculas: {string.uppercase(nombre)}")
```

Salida:

```
Ana tiene 20 años
El doble es 40
Mayúsculas: ANA
```

### Entrada con y sin texto de ayuda

```nexis
// doc: input Ana|7|7
string nombre = Console.input(text="Nombre: ")
int numero = Console.input("Numero: ")
int otro = Console.input()

Console.println(fs"{nombre} eligio {numero} y {otro}")
```

Salida:

```
Nombre: Numero: Ana eligio 7 y 7
```

Las tres formas son válidas:

- `Console.input(text="...")`
- `Console.input("...")`
- `Console.input()`

> `Console.print` y `Console.println` son **sentencias**, no expresiones: no
> puedes asignar su resultado.

---

## 8. Programa integrador

Combina las cinco librerías en un pequeño reporte:

```nexis
#inject math;
#inject string;
#inject file;
#inject random;
#inject time;
#inject Vector;

int inicio = time.clock()

// 1) generar datos
Vector<int> ventas = []
for i in 0 .. 5 {
    ventas.add(random.integer(10, 100))
}

// 2) calcular estadisticas
int total = 0
int maximo = ventas[0]
int minimo = ventas[0]
foreach (v in ventas) {
    total = total + v
    maximo = math.max(maximo, v)
    minimo = math.min(minimo, v)
}

double promedio = double(total) / double(ventas.length())

// 3) escribir el reporte
//    Ojo: fs"..." no interpreta \n; concatena con "\n" real.
string reporte = "total=" + total + "\n" +
                 "promedio=" + promedio + "\n" +
                 "max=" + maximo + "\n" +
                 "min=" + minimo + "\n"
file.write("doc_reporte.txt", reporte)

// 4) leerlo y analizarlo
string leido = file.read("doc_reporte.txt")
Vector<string> lineas = string.split(leido, "\n")
int no_vacias = 0
foreach (l in lineas) {
    if (string.length(l) > 0) {
        no_vacias = no_vacias + 1
    }
}

int fin = time.clock()

Console.println("ventas: " + ventas.length())
Console.println("lineas: " + no_vacias)
Console.println("promedio en rango: " + (promedio >= 10 && promedio <= 100))
Console.println("max >= min: " + (maximo >= minimo))
Console.println("tiempo valido: " + (fin >= inicio))
Console.println("mayusculas: " + string.uppercase("reporte"))
```

Salida:

```
ventas: 6
lineas: 4
promedio en rango: true
max >= min: true
tiempo valido: true
mayusculas: REPORTE
```

> El ejemplo escribe `doc_ejemplo.txt`, `doc_lineas.txt` y `doc_reporte.txt`
> en el directorio de ejecución; el runner de documentación los borra al
> terminar.
