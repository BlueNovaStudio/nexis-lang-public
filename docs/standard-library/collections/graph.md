# Grafo (Graph) en Nexis

Un `Graph<T>` representa vértices identificados por valores de tipo `T` y las conexiones entre ellos. Puede representar rutas dirigidas o no dirigidas.

## 1. Importación

```
#inject graph;
```

## 2. Declaración

```
Graph<string> rutas_aereas = Graph()
```

## 3. Métodos

### `agregar_nodo(valor)`
Añade un vértice al grafo.

### `conectar(origen, destino, peso)`
Conecta dos vértices y guarda un peso opcional.

### `desconectar(origen, destino)`
Elimina una conexión.

### `adyacentes(valor)`
Devuelve los vértices conectados a un nodo.

### `recorrido_anchura(origen)` y `recorrido_profundidad(origen)`
Recorren el grafo usando BFS y DFS.

```
rutas_aereas.agregar_nodo("Lima")
rutas_aereas.agregar_nodo("Cusco")
rutas_aereas.conectar("Lima", "Cusco", 1.5)
```

## 4. Ejemplo completo

```
#inject graph;

Graph<string> rutas_aereas = Graph()
rutas_aereas.agregar_nodo("Lima")
rutas_aereas.agregar_nodo("Cusco")
rutas_aereas.agregar_nodo("Arequipa")
rutas_aereas.conectar("Lima", "Cusco", 1.5)
rutas_aereas.conectar("Cusco", "Arequipa", 1.0)
```

## 5. Complejidad

| Método | Complejidad |
|--------|-------------|
| `agregar_nodo(valor)` | O(1) |
| `conectar(origen, destino, peso)` | O(1) |
| `adyacentes(valor)` | O(1) |
| `recorrido_anchura(origen)` | O(V + E) |
| `recorrido_profundidad(origen)` | O(V + E) |
