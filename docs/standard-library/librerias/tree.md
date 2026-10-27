# Librería Tree en Nexis

`Tree<T>` es un árbol binario de búsqueda: mantiene los elementos
ordenados y permite insertar, buscar y eliminar de forma eficiente.

## 1. Importación

```
#inject Tree;
```

## 2. Declaración e inicialización

```
Tree<int> vacio = []
Tree<int> jerarquia = [50, 25, 75, 10, 30]
Tree<string> nombres = ["Luis", "Ana", "Eva"]
```

El literal se inserta en el árbol; el recorrido interno queda ordenado.

## 3. Acceso por índice

El acceso por índice recorre el árbol **en orden**:

```
Tree<int> t = [50, 25, 75, 10, 30]
Console.println(t[0])   // 10 (el menor)
Console.println(t[4])   // 75 (el mayor)
```

Un índice inválido produce `NX11`.

## 4. Métodos

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `insert(valor)` / `insertar` | `T` | `void` | Inserta manteniendo el orden. |
| `search(valor)` / `contains` / `buscar` / `contiene` | `T` | `bool` | Comprueba si existe. |
| `remove(valor)` / `eliminar` | `T` | `void` | Elimina el valor si existe. |
| `inOrder()` / `en_orden` | — | `void` | Imprime los valores en orden. |
| `length()` / `longitud` | — | `int` | Número de elementos. |
| `isEmpty()` / `esta_vacio` | — | `bool` | `true` si está vacío. |

## 5. Ejemplo completo

```
#inject Tree;

Tree<int> t = []
t.insert(50)
t.insert(25)
t.insert(75)
t.insert(10)
t.insert(30)

Console.println(t.contains(30))   // true
Console.println(t.contains(99))   // false
Console.println(t.length())       // 5

t.inOrder()
// 10
// 25
// 30
// 50
// 75

t.remove(25)
Console.println(t.length())       // 4
```

## 6. Recorrido con foreach

`foreach` sobre un `Tree` entrega los valores en orden ascendente:

```
Tree<string> nombres = ["Luis", "Ana", "Eva"]
foreach (nombre in nombres) {
    Console.println(nombre)
}
// Ana
// Eva
// Luis
```

## 7. Cuándo usarlo

- Búsquedas ordenadas frecuentes.
- Datos que deben mantenerse ordenados sin llamar a `sort()`.
- Recorridos en orden (menor → mayor).

Si solo necesitas una colección ordenada simple, un `Set` también
mantiene unicidad; `Tree` es útil cuando el orden es parte del problema.

## 8. Errores comunes

| Error | Código | Solución |
|-------|--------|----------|
| Índice fuera de rango | `NX11` | Usar `0 ... t.length()`. |
| Esperar duplicados | — | `Tree` no almacena valores repetidos. |
| Mezclar tipos | `NX07` | Un solo tipo por árbol. |

## 9. Complejidad

Inserción, búsqueda y eliminación son O(log n) promedio. El recorrido
completo es O(n).
