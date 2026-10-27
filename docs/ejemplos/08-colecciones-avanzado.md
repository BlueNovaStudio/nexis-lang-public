# 🧩 Colecciones avanzadas: parte 2

Continuación de [02-colecciones.md](02-colecciones.md): `Map`, `Tree`, `Trie`,
`Graph` y la guía para elegir la estructura correcta.

---

## 6. `Map<K, V>` — claves y valores

`foreach` sobre un `Map` entrega las **claves**; el orden de iteración no está
garantizado.

```nexis
#inject Map;
#inject Vector;

Map<string, int> edades = {"Ana": 20, "Luis": 25}

edades.put("Eva", 30)
Console.println(edades.length())
Console.println(edades.get("Ana"))
Console.println(edades.contains("Luis"))
Console.println(edades.contains("Pedro"))

// actualizar una clave existente
edades.set("Ana", 21)
Console.println(edades.get("Ana"))

edades.remove("Luis")
Console.println(edades.length())

Vector<string> claves = edades.keys()
Vector<int> valores = edades.values()
Console.println(claves.length())
Console.println(valores.length())

Console.println(edades.isEmpty())
```

Salida:

```
3
20
true
false
21
2
2
2
false
```

### Ejemplo real: frecuencia de palabras

```nexis
#inject Map;
#inject Vector;
#inject string;

string frase = "el gato y el perro y el gato"
Vector<string> palabras = string.split(frase, " ")
Map<string, int> frecuencia = {}

foreach (p in palabras) {
    if (frecuencia.contains(p)) {
        frecuencia.put(p, frecuencia.get(p) + 1)
    } else {
        frecuencia.put(p, 1)
    }
}

Console.println(frecuencia.get("el"))
Console.println(frecuencia.get("gato"))
Console.println(frecuencia.get("perro"))
Console.println(frecuencia.get("y"))
```

Salida:

```
3
2
1
2
```

### Recorrer claves y valores

```nexis
#inject Map;
#inject Vector;

Map<string, int> stock = {"pan": 10, "leche": 5, "huevos": 12}

// foreach sobre un Map entrega las claves (en cualquier orden)
int total = 0
foreach (clave in stock) {
    total = total + stock.get(clave)
}
Console.println("claves: " + stock.length())
Console.println("total: " + total)

// Para un orden estable, ordena el vector de claves
Vector<string> claves = stock.keys()
claves.sort()
foreach (c in claves) {
    Console.println("ordenada: " + c + " -> " + stock.get(c))
}
```

Salida:

```
claves: 3
total: 27
ordenada: huevos -> 12
ordenada: leche -> 5
ordenada: pan -> 10
```

> La primera parte no depende del orden de iteración; la segunda siempre sale
> ordenada porque se ordena el vector de claves.

---

## 7. `Tree<T>` — árbol binario de búsqueda

Mantiene los elementos ordenados. `inOrder()` los imprime de menor a mayor.

```nexis
#inject Tree;

Tree<int> t = [50, 25, 75, 10]

Console.println(t.length())
Console.println(t.isEmpty())
Console.println(t.contains(25))
Console.println(t.contains(99))

t.insert(30)
Console.println(t.length())

t.remove(25)
Console.println(t.length())

// índice = recorrido en orden
Console.println(t[0])
Console.println(t[t.length() - 1])
```

Salida:

```
4
false
true
false
5
4
10
75
```

### Recorrido ordenado

```nexis
#inject Tree;

Tree<int> t = []
t.insert(50)
t.insert(25)
t.insert(75)
t.insert(10)
t.insert(30)

t.inOrder()

Console.println("--- foreach ---")
foreach (n in t) {
    Console.println(n)
}
```

Salida:

```
10
25
30
50
75
--- foreach ---
10
25
30
50
75
```

---

## 8. `Trie` — árbol de prefijos

`Trie` no lleva parámetro de tipo: siempre guarda cadenas.

```nexis
#inject Trie;
#inject Vector;

Trie dic = Trie()
dic.insert("casa")
dic.insert("casamiento")
dic.insert("casual")
dic.insert("perro")

Console.println(dic.contains("casa"))
Console.println(dic.contains("cas"))
Console.println(dic.startsWith("cas"))
Console.println(dic.startsWith("zzz"))

Vector<string> coincidencias = dic.searchPrefix("cas")
Console.println(coincidencias)
```

Salida:

```
true
false
true
false
[casa, casamiento, casual]
```

### Autocompletado

```nexis
#inject Trie;
#inject Vector;

Trie palabras = Trie()
palabras.insert("Nexis")
palabras.insert("Nexo")
palabras.insert("Nube")

Vector<string> sugerencias = palabras.searchPrefix("Ne")
foreach (s in sugerencias) {
    Console.println(s)
}
```

Salida:

```
Nexis
Nexo
```

---

## 9. `Graph<T>` — grafo dirigido con pesos

```nexis
#inject Graph;
#inject Vector;

Graph<string> red = Graph()
red.addNode("Lima")
red.addNode("Cusco")
red.addNode("Arequipa")

red.connect("Lima", "Cusco", 1100)
red.connect("Lima", "Arequipa", 1000)
red.connect("Arequipa", "Cusco", 500)

Console.println(red.length())
Console.println(red.isEmpty())

Vector<string> vecinos = red.neighbors("Lima")
Console.println(vecinos)

red.disconnect("Lima", "Arequipa")
Console.println(red.neighbors("Lima").length())
```

Salida:

```
3
false
[Arequipa, Cusco]
1
```

### Recorridos BFS y DFS

```nexis
#inject Graph;

Graph<int> g = Graph()
g.addNode(1)
g.addNode(2)
g.addNode(3)
g.addNode(4)

g.connect(1, 2, 1)
g.connect(1, 3, 1)
g.connect(2, 4, 1)

Console.println("BFS")
g.breadthFirst(1)

Console.println("DFS")
g.depthFirst(1)
```

Salida:

```
BFS
1
2
3
4
DFS
1
2
4
3
```

> Las aristas son **dirigidas**: `connect(a, b)` va de `a` a `b`. Para una
> conexión en ambos sentidos, llama dos veces.

---

## 10. ¿Qué estructura usar?

| Necesitas | Usa | Motivo |
|-----------|-----|--------|
| Acceso por índice y orden | `Vector` | O(1) por índice, `sort()` incluido |
| Insertar/eliminar en extremos | `LinkedList` | O(1) en los extremos |
| Último en entrar, primero en salir | `Stack` | LIFO con `push`/`pop` |
| Primero en entrar, primero en salir | `Queue` | FIFO con `enqueue`/`dequeue` |
| Sin duplicados y pertenencia rápida | `Set` | `contains` O(1) promedio |
| Clave → valor | `Map` | `put`/`get` O(1) promedio |
| Datos siempre ordenados | `Tree` | Recorrido en orden O(n) |
| Búsqueda por prefijo | `Trie` | O(longitud de la palabra) |
| Nodos y conexiones | `Graph` | BFS/DFS incluidos |

### Combinarlas en un mismo programa

```nexis
#inject Vector;
#inject Map;
#inject Set;
#inject Queue;

Vector<string> pedidos = ["pan", "leche", "pan", "cafe"]
Set<string> unicos = {}
Map<string, int> conteo = {}
Queue<string> pendientes = []

foreach (p in pedidos) {
    unicos.add(p)
    if (conteo.contains(p)) {
        conteo.put(p, conteo.get(p) + 1)
    } else {
        conteo.put(p, 1)
    }
    pendientes.enqueue(p)
}

Console.println("pedidos: " + pedidos.length())
Console.println("únicos: " + unicos.length())
Console.println("pan: " + conteo.get("pan"))

int procesados = 0
while (!pendientes.isEmpty()) {
    pendientes.dequeue()
    procesados = procesados + 1
}
Console.println("procesados: " + procesados)
```

Salida:

```
pedidos: 4
únicos: 3
pan: 2
procesados: 4
```