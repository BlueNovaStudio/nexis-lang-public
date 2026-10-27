# Librería Set en Nexis

`Set<T>` es un conjunto de valores **únicos**, sin claves asociadas. Se
usa para eliminar duplicados y comprobar pertenencia.

## 1. Importación

```
#inject Set;
```

## 2. Declaración e inicialización

```
Set<int> vacio = {}
Set<int> ids = {10, 15, 20}
Set<string> nombres = {"Ana", "Luis", "Ana"}   // queda {"Ana", "Luis"}
```

Las llaves **sin `:`** representan un conjunto; las llaves **con `:`**
representan un mapa (`Map<K, V>`).

## 3. Acceso por índice

El orden interno no está garantizado. Para que el acceso por índice sea
determinista, Nexis ordena la representación antes de indexar:

```
Set<int> ids = {30, 10, 20}
Console.println(ids[0])   // 10
Console.println(ids[2])   // 30
```

No se recomienda usar índices para lógica de negocio; usa `contains` o
`foreach`.

## 4. Métodos

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `add(valor)` / `agregar` | `T` | `void` | Añade si no existe. |
| `remove(valor)` / `eliminar` | `T` | `void` | Elimina si existe. |
| `contains(valor)` / `contiene` | `T` | `bool` | Comprueba pertenencia. |
| `length()` / `longitud` | — | `int` | Número de elementos. |
| `isEmpty()` / `esta_vacio` | — | `bool` | `true` si está vacío. |

## 5. Ejemplo: eliminar duplicados

```
#inject Set;
#inject Vector;

Vector<int> numeros = [1, 2, 2, 3, 3, 3, 4]
Set<int> unicos = {}

foreach (n in numeros) {
    unicos.add(n)
}

Console.println(unicos.length())   // 4
Console.println(unicos.contains(3)) // true

foreach (n in unicos) {
    Console.println(n)
}
```

## 6. Ejemplo: intersección manual

```
#inject Set;
#inject Vector;

Set<int> a = {1, 2, 3, 4}
Set<int> b = {3, 4, 5}
Vector<int> comunes = []

foreach (n in a) {
    if (b.contains(n)) {
        comunes.add(n)
    }
}
Console.println(comunes)   // [3, 4]
```

## 7. Errores comunes

| Error | Código | Solución |
|-------|--------|----------|
| Mezclar tipos en el conjunto | `NX07` | Un solo tipo por `Set`. |
| Esperar orden de inserción | — | Usar `Vector` si el orden importa. |
| Índice fuera de rango | `NX11` | Usar `foreach` o comprobar `length()`. |

## 8. Complejidad

`add`, `remove` y `contains` son O(1) promedio. `length` e `isEmpty` son
O(1). El acceso por índice implica ordenar: O(n log n).
