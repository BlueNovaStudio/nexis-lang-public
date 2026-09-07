# Librería Graph en Nexis

Proporciona el grafo `Graph<T>`, formado por vértices y conexiones.

## Importación

```
#inject graph;
```

## Declaración y uso

```
Graph<string> rutas = Graph()
rutas.agregar_nodo("Lima")
rutas.conectar("Lima", "Cusco", 1.5)
```

## Operaciones principales

- `agregar_nodo(valor)` añade un vértice.
- `conectar(origen, destino, peso)` crea una conexión.
- `desconectar(origen, destino)` elimina una conexión.
- `adyacentes(valor)` consulta vecinos.
- `recorrido_anchura(origen)` y `recorrido_profundidad(origen)` recorren el grafo.

Consulta [la documentación completa de Graph](../collections/graph.md).
