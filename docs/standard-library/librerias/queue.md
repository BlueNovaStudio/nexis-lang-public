# Librería Queue en Nexis

`Queue<T>` es una cola con comportamiento **FIFO** (*First In, First
Out*): el primer elemento que entra es el primero que sale.

## 1. Importación

```
#inject Queue;
```

## 2. Declaración e inicialización

```
Queue<int> vacia = []
Queue<string> turnos = ["Ana", "Luis", "Eva"]
```

El primer elemento del literal es el frente de la cola.

## 3. Acceso por índice

```
Queue<int> cola = [8, 6, 10]
Console.println(cola[0])   // 8
cola[0] = 1                // [1, 6, 10]
```

El índice `0` es el frente. Un índice inválido produce `NX11`.

## 4. Métodos

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `enqueue(valor)` / `encolar` | `T` | `void` | Añade al final. |
| `dequeue()` / `desencolar` | — | `T` | Quita y devuelve el frente. |
| `front()` / `peek()` / `frente` | — | `T` | Consulta el frente sin quitarlo. |
| `get(indice)` / `obtener` | `int` | `T` | Lee por posición. |
| `sort()` / `ordenar` | — | `void` | Ordena de frente a final. |
| `reverse()` / `invertir` | — | `void` | Invierte el orden. |
| `length()` / `longitud` | — | `int` | Número de elementos. |
| `isEmpty()` / `esta_vacio` | — | `bool` | `true` si está vacía. |

`dequeue` y `front` lanzan `NX50` si la cola está vacía.

## 5. Ejemplo: simular una fila de atención

```
#inject Queue;

Queue<string> fila = []
fila.enqueue("Ana")
fila.enqueue("Luis")
fila.enqueue("Eva")

while (!fila.isEmpty()) {
    Console.println("Atendiendo a " + fila.dequeue())
}
// Atendiendo a Ana
// Atendiendo a Luis
// Atendiendo a Eva
```

## 6. Ejemplo: recorrido por niveles (BFS)

```
#inject Queue;

Queue<int> pendientes = []
pendientes.enqueue(1)

while (!pendientes.isEmpty()) {
    int actual = pendientes.dequeue()
    Console.println(actual)
    if (actual * 2 <= 8) {
        pendientes.enqueue(actual * 2)
    }
}
// 1, 2, 4, 8
```

## 7. Errores comunes

| Error | Código | Solución |
|-------|--------|----------|
| Desencolar vacía | `NX50` | Comprobar `isEmpty()`. |
| Consultar frente vacío | `NX50` | Comprobar `isEmpty()`. |
| Índice inválido | `NX11` | Usar `0 ... length()`. |
| Esperar orden LIFO | — | Usar `Stack`. |

## 8. Complejidad

`enqueue`, `dequeue`, `front`, `length` e `isEmpty` son O(1). `sort` es
O(n log n); `reverse` es O(n).
