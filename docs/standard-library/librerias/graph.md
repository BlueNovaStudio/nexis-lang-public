# Librería Graph en Nexis

`Graph<T>` representa un grafo dirigido con pesos: cada nodo puede tener
vecinos y cada conexión tiene un peso numérico.

## 1. Importación

```
#inject Graph;
```

## 2. Declaración e inicialización

```
Graph<string> vacio = Graph()
Graph<string> rutas = Graph()
rutas.addNode("Lima")
rutas.connect("Lima", "Cusco", 1.5)
```

El grafo se construye nodo a nodo; no se inicializa con un literal de
colección.

## 3. Métodos

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `addNode(nodo)` / `agregar_nodo` | `T` | `void` | Añade un vértice. |
| `connect(origen, destino, peso)` / `addEdge` / `conectar` | `T`, `T`, `number` | `void` | Crea una arista dirigida. |
| `disconnect(origen, destino)` / `removeEdge` / `desconectar` | `T`, `T` | `void` | Elimina la arista. |
| `neighbors(nodo)` / `adjacent` / `adyacentes` | `T` | `Vector<T>` | Vecinos del nodo. |
| `breadthFirst(inicio)` / `bfs` / `recorrido_anchura` | `T` | `void` | Recorrido en anchura (imprime). |
| `depthFirst(inicio)` / `dfs` / `recorrido_profundidad` | `T` | `void` | Recorrido en profundidad (imprime). |
| `length()` / `longitud` | — | `int` | Número de nodos. |
| `isEmpty()` / `esta_vacio` | — | `bool` | `true` si no hay nodos. |

El peso es opcional en `connect`; si se omite, se usa `0`.

## 4. Ejemplo: red de ciudades

```
#inject Graph;
#inject Vector;

Graph<string> red = Graph()
red.addNode("Lima")
red.addNode("Cusco")
red.addNode("Arequipa")

red.connect("Lima", "Cusco", 1100)
red.connect("Lima", "Arequipa", 1000)
red.connect("Arequipa", "Cusco", 500)

Console.println(red.length())            // 3
Vector<string> vecinos = red.neighbors("Lima")
Console.println(vecinos)                 // [Cusco, Arequipa]

red.breadthFirst("Lima")
// Lima
// Cusco
// Arequipa
```

## 5. Ejemplo: recorrido en profundidad

```
#inject Graph;

Graph<int> g = Graph()
g.addNode(1)
g.connect(1, 2, 1)
g.connect(1, 3, 1)
g.connect(2, 4, 1)

g.depthFirst(1)
// 1
// 2
// 4
// 3
```

## 6. Dirección de las aristas

`connect(a, b)` crea una arista **de `a` hacia `b`**. Si necesitas una
conexión en ambos sentidos, llama dos veces:

```
g.connect("Lima", "Cusco", 1)
g.connect("Cusco", "Lima", 1)
```

## 7. Errores comunes

| Error | Código | Solución |
|-------|--------|----------|
| Consultar vecinos de un nodo inexistente | — | Devuelve un vector vacío; usa `addNode`. |
| Esperar conexión bidireccional | — | Crear las dos aristas. |
| Mezclar tipos de nodo | `NX07` | Un solo tipo `T` por grafo. |

## 8. Complejidad

`addNode` es O(1). `connect`, `disconnect` y `neighbors` son O(1)
promedio. Los recorridos BFS/DFS son O(V + E).
