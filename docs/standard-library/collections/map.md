# Mapa (Map) en Nexis

Un `Map<K, V>` relaciona claves únicas con valores. Las claves tienen el tipo `K` y los valores el tipo `V`.

## 1. Importación

```
#inject map;
```

## 2. Declaración

```
Map<string, int> inventario = {
	"manzanas": 50,
	"peras": 30
}
```

Las parejas clave-valor se separan con dos puntos (`:`). Las llaves sin dos puntos representan un conjunto.

## 3. Métodos

### `poner(clave, valor)`
Agrega una pareja o reemplaza el valor de una clave existente.

### `obtener(clave)`
Devuelve el valor asociado a una clave.

### `contiene(clave)`
Comprueba si una clave existe.

### `eliminar(clave)` y `longitud()`
Eliminan una pareja y consultan el número de parejas almacenadas.

```
inventario.poner("naranjas", 20)
int cantidad = inventario.obtener("manzanas")
bool existe = inventario.contiene("peras")
```

## 4. Ejemplo completo

```
#inject map;

Map<string, string> capitales = {
	"Peru": "Lima",
	"Chile": "Santiago"
}
capitales.poner("Argentina", "Buenos Aires")
```

## 5. Complejidad

| Método | Complejidad promedio |
|--------|----------------------|
| `poner(clave, valor)` | O(1) |
| `obtener(clave)` | O(1) |
| `contiene(clave)` | O(1) |
| `eliminar(clave)` | O(1) |
