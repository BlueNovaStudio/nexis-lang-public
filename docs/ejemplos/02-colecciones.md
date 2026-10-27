# 🗃️ Colecciones: todas las estructuras y todos sus métodos

Parte 1 (secciones 1 a 5): `Vector`, `LinkedList`, `Stack`, `Queue` y `Set`.
La **parte 2** (`Map`, `Tree`, `Trie`, `Graph` y la guía para elegir) continúa en
[08-colecciones-avanzado.md](08-colecciones-avanzado.md).

Nexis incluye nueve estructuras de datos. Todas son **genéricas**
(`Estructura<Tipo>`), se inicializan con literales o con el constructor vacío y
se recorren con `foreach`.

Las firmas completas están en la [referencia rápida](../referencia-rapida.md) y
en la [referencia API](../referencia-api.md); aquí tienes un ejemplo ejecutable
de **cada método**.

---

## 1. `Vector<T>` — arreglo dinámico

### Creación y acceso por índice

```nexis
#inject Vector;

Vector<int> vacio = []
Vector<string> nombres = ["Ana", "Luis", "Eva"]
Vector<double> reales = [1.5, 2.5]
Vector<Vector<int>> matriz = [[1, 2], [3, 4]]

Console.println(vacio)
Console.println(nombres.length())
Console.println(reales[1])
Console.println(matriz[1][0])

// escritura por índice
nombres[1] = "Lucas"
Console.println(nombres)
```

Salida:

```
[]
3
2.5
3
[Ana, Lucas, Eva]
```

### `add`, `insert`, `get`, `set`

```nexis
#inject Vector;

Vector<int> v = [5, 1, 4]
v.add(2)
Console.println(v)

v.insert(0, 9)
Console.println(v)

Console.println(v.get(2))
v.set(2, 99)
Console.println(v)
```

Salida:

```
[5, 1, 4, 2]
[9, 5, 1, 4, 2]
1
[9, 5, 99, 4, 2]
```

### `first`, `last`, `contains`, `indexOf`, `lastIndexOf`

```nexis
#inject Vector;

Vector<int> v = [1, 2, 1, 3, 1]

Console.println(v.first())
Console.println(v.last())
Console.println(v.contains(3))
Console.println(v.contains(7))
Console.println(v.indexOf(1))
Console.println(v.lastIndexOf(1))
Console.println(v.indexOf(7))
```

Salida:

```
1
1
true
false
0
4
-1
```

### `remove`, `pop`, `clear`

```nexis
#inject Vector;

Vector<int> v = [10, 20, 30, 40]
v.remove(1)
Console.println(v)

int ultimo = v.pop()
Console.println(ultimo)
Console.println(v)

v.clear()
Console.println(v.length())
Console.println(v.isEmpty())
```

Salida:

```
[10, 30, 40]
40
[10, 30]
0
true
```

### `sort`, `reverse`, `length`, `isEmpty`

```nexis
#inject Vector;

Vector<int> v = [5, 1, 4, 2, 3]
Console.println(v.length())
Console.println(v.isEmpty())

v.sort()
Console.println(v)

v.reverse()
Console.println(v)
```

Salida:

```
5
false
[1, 2, 3, 4, 5]
[5, 4, 3, 2, 1]
```

### Recorrido: `foreach` y `for` con índice

```nexis
#inject Vector;

Vector<string> frutas = ["manzana", "pera", "uva"]

foreach (f in frutas) {
    Console.println(f)
}

for i in 0 ... frutas.length() {
    Console.println(fs"{i}: {frutas[i]}")
}
```

Salida:

```
manzana
pera
uva
0: manzana
1: pera
2: uva
```

### Pasar un `Vector` a una función

Los vectores se pasan con **copia de salida**: la función los modifica y el
llamador conserva los cambios.

```nexis
#inject Vector;

void ordenar(Vector<int>: v) -> void {
    v.sort()
}

void duplicar(Vector<int>: v) -> void {
    for i in 0 ... v.length() {
        v[i] = v[i] * 2
    }
}

Vector<int> datos = [3, 1, 2]
ordenar(datos)
Console.println(datos)

duplicar(datos)
Console.println(datos)
```

Salida:

```
[1, 2, 3]
[2, 4, 6]
```

### Matrices: `Vector<Vector<T>>`

```nexis
#inject Vector;

Vector<Vector<int>> m = [[1, 2, 3], [4, 5, 6]]

for i in 0 ... m.length() {
    int suma = 0
    for j in 0 ... m[i].length() {
        suma = suma + m[i][j]
    }
    Console.println(fs"fila {i} suma {suma}")
}

Console.println(m[1][2])
```

Salida:

```
fila 0 suma 6
fila 1 suma 15
6
```

---

## 2. `LinkedList<T>` — lista doblemente enlazada

```nexis
#inject LinkedList;

LinkedList<int> l = [5, 3, 9]

l.add(7)
Console.println(l)

l.addFirst(1)
l.addLast(11)
Console.println(l)

Console.println(l.get(1))
l.set(1, 33)
Console.println(l)

Console.println(l.first())
Console.println(l.last())
Console.println(l.contains(9))
Console.println(l.indexOf(9))
```

Salida:

```
[5, 3, 9, 7]
[1, 5, 3, 9, 7, 11]
5
[1, 33, 3, 9, 7, 11]
1
11
true
3
```

### Eliminar por extremos y por índice

```nexis
#inject LinkedList;

LinkedList<int> l = [1, 2, 3, 4, 5]

Console.println(l.removeFirst())
Console.println(l.removeLast())
Console.println(l)

l.remove(0)
Console.println(l)

l.sort()
Console.println(l)

l.reverse()
Console.println(l)

Console.println(l.length())
Console.println(l.isEmpty())
Console.println(l[0])
```

Salida:

```
1
5
[2, 3, 4]
[3, 4]
[3, 4]
[4, 3]
2
false
4
```

### Uso típico: cola de historial

```nexis
#inject LinkedList;

LinkedList<string> historial = []

historial.addLast("inicio")
historial.addLast("perfil")
historial.addLast("ajustes")

while (!historial.isEmpty()) {
    Console.println("Visita: " + historial.removeFirst())
}
```

Salida:

```
Visita: inicio
Visita: perfil
Visita: ajustes
```

---

## 3. `Stack<T>` — pila LIFO

```nexis
#inject Stack;

Stack<int> pila = [1, 2, 3]

pila.push(4)
Console.println(pila)

Console.println(pila.peek())
Console.println(pila.top())
Console.println(pila.get(0))

Console.println(pila.pop())
Console.println(pila)

pila.sort()
Console.println(pila)

pila.reverse()
Console.println(pila)

Console.println(pila.length())
Console.println(pila.isEmpty())
```

Salida:

```
[1, 2, 3, 4]
4
4
1
4
[1, 2, 3]
[1, 2, 3]
[3, 2, 1]
3
false
```

### Ejemplo real: paréntesis balanceados

```nexis
#inject Stack;

string expresion = "(a+b)*(c-d)"
Stack<char> pila = []
bool balanceado = true

foreach (char c, expresion) {
    if (c == '(') {
        pila.push(c)
    } else if (c == ')') {
        if (pila.isEmpty()) {
            balanceado = false
        } else {
            pila.pop()
        }
    }
}

if (!pila.isEmpty()) {
    balanceado = false
}

Console.println(balanceado)
```

Salida:

```
true
```

---

## 4. `Queue<T>` — cola FIFO

```nexis
#inject Queue;

Queue<int> cola = [1, 2, 3]

cola.enqueue(4)
Console.println(cola)

Console.println(cola.front())
Console.println(cola.peek())
Console.println(cola.get(0))

Console.println(cola.dequeue())
Console.println(cola)

cola.sort()
Console.println(cola)

cola.reverse()
Console.println(cola)

Console.println(cola.length())
Console.println(cola.isEmpty())
```

Salida:

```
[1, 2, 3, 4]
1
1
1
1
[2, 3, 4]
[2, 3, 4]
[4, 3, 2]
3
false
```

### Ejemplo real: fila de atención

```nexis
#inject Queue;

Queue<string> fila = []
fila.enqueue("Ana")
fila.enqueue("Luis")
fila.enqueue("Eva")

while (!fila.isEmpty()) {
    Console.println("Atendiendo a " + fila.dequeue())
}
```

Salida:

```
Atendiendo a Ana
Atendiendo a Luis
Atendiendo a Eva
```

---

## 5. `Set<T>` — conjunto sin duplicados

El orden interno no está garantizado; el **acceso por índice** usa el orden
ordenado, y para lógica de negocio conviene usar `contains` o `foreach`.

```nexis
#inject Set;

Set<int> s = {30, 10, 20, 10}

Console.println(s.length())
Console.println(s.contains(20))
Console.println(s.contains(99))

// acceso por índice: ordenado de menor a mayor
Console.println(s[0])
Console.println(s[1])
Console.println(s[2])

s.add(40)
s.add(10)
Console.println(s.length())

s.remove(30)
Console.println(s.length())
Console.println(s.isEmpty())
```

Salida:

```
3
true
false
10
20
30
4
3
false
```

### Ejemplo real: eliminar duplicados

```nexis
#inject Set;
#inject Vector;

Vector<int> numeros = [1, 2, 2, 3, 3, 3, 4]
Set<int> unicos = {}

foreach (n in numeros) {
    unicos.add(n)
}

Console.println(unicos.length())
Console.println(unicos.contains(3))
```

Salida:

```
4
true
```

### Unión e intersección manual

```nexis
#inject Set;
#inject Vector;

Set<int> a = {1, 2, 3, 4}
Set<int> b = {3, 4, 5}

Set<int> union = {}
foreach (n in a) { union.add(n) }
foreach (n in b) { union.add(n) }

Vector<int> comunes = []
foreach (n in a) {
    if (b.contains(n)) {
        comunes.add(n)
    }
}
comunes.sort()

Console.println(union.length())
Console.println(comunes)
```

Salida:

```
5
[3, 4]
```

---

> Las secciones 6 a 10 (`Map`, `Tree`, `Trie`, `Graph` y la guía para elegir)
> continúan en [08-colecciones-avanzado.md](08-colecciones-avanzado.md).