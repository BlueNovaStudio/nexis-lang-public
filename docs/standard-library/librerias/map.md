# Librería Map en Nexis

Proporciona el mapa `Map<K, V>`, una colección de parejas clave-valor.

## Importación

```
#inject map;
```

## Declaración y uso

```
Map<string, int> inventario = {"manzanas": 50}
inventario.poner("peras", 30)
int cantidad = inventario.obtener("manzanas")
```

## Operaciones principales

- `poner(clave, valor)` crea o actualiza una pareja.
- `obtener(clave)` devuelve el valor asociado.
- `contiene(clave)` comprueba la existencia de una clave.
- `eliminar(clave)` y `longitud()` gestionan y consultan el mapa.

Consulta [la documentación completa de Map](../collections/map.md).
