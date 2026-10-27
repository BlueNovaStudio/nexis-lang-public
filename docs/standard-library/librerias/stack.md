# Librería Stack en Nexis

`Stack<T>` es una pila con comportamiento **LIFO** (*Last In, First Out*):
el último elemento que entra es el primero que sale.

## 1. Importación

```
#inject Stack;
```

## 2. Declaración e inicialización

```
Stack<int> vacia = []
Stack<string> historial = ["inicio", "menu"]
```

El último elemento del literal queda en la cima.

## 3. Acceso por índice

```
Stack<int> pila = [3, 1, 2]
Console.println(pila[0])   // 3
pila[0] = 9                // [9, 1, 2]
```

El índice `0` es el fondo y `length() - 1` la cima. Un índice inválido
produce `NX11`.

## 4. Métodos

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `push(valor)` / `apilar` | `T` | `void` | Apila en la cima. |
| `pop()` / `desapilar` | — | `T` | Desapila y devuelve la cima. |
| `peek()` / `top()` / `cima` | — | `T` | Consulta la cima sin quitarla. |
| `get(indice)` / `obtener` | `int` | `T` | Lee por posición. |
| `sort()` / `ordenar` | — | `void` | Ordena de fondo a cima. |
| `reverse()` / `invertir` | — | `void` | Invierte el orden. |
| `length()` / `longitud` | — | `int` | Número de elementos. |
| `isEmpty()` / `esta_vacio` | — | `bool` | `true` si está vacía. |

`pop` y `peek` lanzan `NX50` si la pila está vacía.

## 5. Ejemplo: comprobar paréntesis balanceados

```
#inject Stack;

string expresion = "(a+b)*(c-d)"
Stack<char> pila = []
bool balanceado = true

foreach (char c, expresion) {
    if (c == '(') {
        pila.push(c)
    } else if (c == ')') {
        if (pila.isEmpty()) {
            balanceado = false
        } else {
            pila.pop()
        }
    }
}

if (!pila.isEmpty()) {
    balanceado = false
}

Console.println(balanceado)   // true
```

## 6. Ejemplo: deshacer acciones

```
#inject Stack;

Stack<string> acciones = []
acciones.push("escribir")
acciones.push("borrar")
acciones.push("pegar")

while (!acciones.isEmpty()) {
    Console.println("Deshacer: " + acciones.pop())
}
// Deshacer: pegar
// Deshacer: borrar
// Deshacer: escribir
```

## 7. Errores comunes

| Error | Código | Solución |
|-------|--------|----------|
| Desapilar vacía | `NX50` | Comprobar `isEmpty()`. |
| Consultar cima vacía | `NX50` | Comprobar `isEmpty()`. |
| Índice inválido | `NX11` | Usar `0 ... length()`. |
| Esperar orden FIFO | — | Usar `Queue`. |

## 8. Complejidad

`push`, `pop`, `peek`, `length` e `isEmpty` son O(1). `sort` es
O(n log n); `reverse` es O(n).
