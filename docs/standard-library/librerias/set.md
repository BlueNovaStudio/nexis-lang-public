# Librería Set en Nexis

Proporciona el conjunto `Set<T>`, una colección de valores únicos.

## Importación

```
#inject set;
```

## Declaración y uso

```
Set<int> ids = {10, 15, 20}
ids.agregar(25)
bool activo = ids.contiene(15)
```

Las llaves sin `:` representan un conjunto; las llaves con `:` representan un mapa.

## Operaciones principales

- `agregar(valor)` añade un valor si no existe.
- `eliminar(valor)` elimina un valor.
- `contiene(valor)` comprueba la existencia.
- `longitud()` y `esta_vacio()` consultan el estado.

Consulta [la documentación completa de Set](../collections/set.md).
