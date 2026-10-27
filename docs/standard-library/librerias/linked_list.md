# Librería LinkedList en Nexis

`LinkedList<T>` es una lista doblemente enlazada. Permite insertar y
eliminar en los extremos en O(1) y recorrer los elementos en orden.

En Nexis se implementa sobre una cola doble (`VecDeque`), por lo que
también admite acceso por índice O(1) además de las operaciones de
extremos.

## 1. Importación

```
#inject LinkedList;
```

## 2. Declaración e inicialización

```
LinkedList<int> vacia = []
LinkedList<int> lista = [5, 3, 9, 1]
LinkedList<string> nombres = ["Ana", "Luis"]
```

## 3. Acceso por índice

```
LinkedList<int> lista = [5, 3, 9, 1]
Console.println(lista[0])   // 5
lista[1] = 7                // [5, 7, 9, 1]
```

Un índice inválido produce `NX11`.

## 4. Métodos

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `add(valor)` / `agregar` | `T` | `void` | Añade al final. |
| `addFirst(valor)` / `agregar_frente` | `T` | `void` | Añade al inicio. |
| `addLast(valor)` / `agregar_fondo` | `T` | `void` | Añade al final. |
| `removeFirst()` / `eliminar_frente` | — | `T` | Elimina y devuelve el primero. |
| `removeLast()` / `eliminar_fondo` | — | `T` | Elimina y devuelve el último. |
| `remove(indice)` / `eliminar` | `int` | `void` | Elimina por posición. |
| `get(indice)` / `obtener` | `int` | `T` | Lee por posición. |
| `set(indice, valor)` / `asignar` | `int`, `T` | `void` | Modifica por posición. |
| `first()` / `primero` | — | `T` | Primer elemento. |
| `last()` / `ultimo` | — | `T` | Último elemento. |
| `contains(valor)` / `contiene` | `T` | `bool` | Comprueba existencia. |
| `indexOf(valor)` / `indice_de` | `T` | `int` | Posición o `-1`. |
| `sort()` / `ordenar` | — | `void` | Orden ascendente. |
| `reverse()` / `invertir` | — | `void` | Invierte el orden. |
| `length()` / `longitud` | — | `int` | Número de elementos. |
| `isEmpty()` / `esta_vacio` | — | `bool` | `true` si está vacía. |

Los métodos de extremos (`removeFirst`, `removeLast`) lanzan `NX50` si la
lista está vacía. `get`, `set` y `remove` lanzan `NX11` con índice
inválido.

## 5. Ejemplo completo

```
#inject LinkedList;

LinkedList<int> lista = [5, 3, 9, 1]

lista.addFirst(10)
Console.println(lista)        // [10, 5, 3, 9, 1]

lista.addLast(7)
Console.println(lista)        // [10, 5, 3, 9, 1, 7]

lista.sort()
Console.println(lista)        // [1, 3, 5, 7, 9, 10]

lista.reverse()
Console.println(lista)        // [10, 9, 7, 5, 3, 1]

int primero = lista.removeFirst()
int ultimo = lista.removeLast()
Console.println(primero)      // 10
Console.println(ultimo)       // 1
Console.println(lista)        // [9, 7, 5, 3]
```

## 6. Ordenar con acceso por índice

```
#inject LinkedList;

LinkedList<int> lista = [64, 34, 25, 12, 22, 11, 90]
int n = lista.length()
for i in 0 ... n {
    for j in 0 ... (n - i - 1) {
        if (lista[j] > lista[j + 1]) {
            int aux = lista[j]
            lista[j] = lista[j + 1]
            lista[j + 1] = aux
        }
    }
}
Console.println(lista)
```

## 7. Cuándo usarla

- Inserciones y eliminaciones frecuentes en los extremos.
- Recorridos secuenciales.
- Implementar pilas, colas o buffers.

Si necesitas acceso aleatorio intensivo, `Vector` suele ser más simple.

## 8. Errores comunes

| Error | Código | Solución |
|-------|--------|----------|
| Índice fuera de rango | `NX11` | Comprobar `length()`. |
| Extraer de lista vacía | `NX50` | Comprobar `isEmpty()`. |
| Confundir `add` con `addFirst` | — | `add` añade al final. |
