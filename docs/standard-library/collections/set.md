# Conjunto (Set) en Nexis

Un `Set<T>` almacena valores únicos y no garantiza un orden de inserción.

## 1. Importación

```
#inject set;
```

## 2. Declaración

```
Set<int> ids_activos = {10, 15, 20}
```

Sin dos puntos (`:`), las llaves representan un conjunto. Con dos puntos representan un mapa.

## 3. Métodos

### `agregar(valor)`
Añade un valor si todavía no existe.

### `eliminar(valor)`
Elimina un valor del conjunto.

### `contiene(valor)`
Devuelve `true` si el valor existe.

### `longitud()` y `esta_vacio()`
Devuelven el tamaño y el estado del conjunto.

```
ids_activos.agregar(25)
bool activo = ids_activos.contiene(15)
ids_activos.eliminar(10)
```

## 4. Ejemplo completo

```
#inject set;

Set<int> ids_activos = {10, 15, 20}
ids_activos.agregar(25)
ids_activos.agregar(25)   // No duplica el valor
```

## 5. Complejidad

| Método | Complejidad promedio |
|--------|----------------------|
| `agregar(valor)` | O(1) |
| `eliminar(valor)` | O(1) |
| `contiene(valor)` | O(1) |
| `longitud()` | O(1) |
