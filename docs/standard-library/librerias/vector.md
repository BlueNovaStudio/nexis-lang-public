# Librería Vector en Nexis

`Vector<T>` es el arreglo dinámico de Nexis: una secuencia ordenada de
elementos del **mismo tipo** que puede crecer y reducirse en tiempo de
ejecución.

- Acceso por índice en O(1).
- Inserción/eliminación en el medio en O(n).
- `sort()` ordena en orden ascendente según el tipo de los elementos.

## 1. Importación

```
#inject Vector;
```

## 2. Declaración e inicialización

```
Vector<int> vacio = []
Vector<string> nombres = ["Ana", "Luis", "Eva"]
Vector<double> reales = [1.5, 2.5, 3.5]
Vector<Vector<int>> matriz = [[1, 2], [3, 4]]
```

También se puede declarar y asignar después:

```
Vector<int> datos = []
datos = [10, 20, 30]
```

## 3. Acceso por índice

```
Vector<int> v = [10, 20, 30]
int primero = v[0]        // 10
v[1] = 99                 // [10, 99, 30]
```

- El índice empieza en `0`.
- Un índice negativo o `>= length()` produce `NX11`.
- `v[i]` equivale a `v.get(i)` para lectura y a `v.set(i, valor)` para
  escritura.

## 4. Métodos

Todos los métodos aceptan su nombre en inglés y en español.

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `add(valor)` / `agregar` | `T` | `void` | Añade al final. |
| `insert(indice, valor)` / `insertar` | `int`, `T` | `void` | Inserta en la posición; `indice == length()` añade al final. |
| `get(indice)` / `obtener` | `int` | `T` | Lee un elemento. |
| `set(indice, valor)` / `asignar` | `int`, `T` | `void` | Modifica un elemento. |
| `remove(indice)` / `eliminar` | `int` | `void` | Elimina y desplaza el resto. |
| `pop()` / `extraer` | — | `T` | Elimina y devuelve el último. |
| `first()` / `primero` | — | `T` | Primer elemento. |
| `last()` / `ultimo` | — | `T` | Último elemento. |
| `contains(valor)` / `contiene` | `T` | `bool` | Comprueba existencia. |
| `indexOf(valor)` / `indice_de` | `T` | `int` | Primera posición o `-1`. |
| `lastIndexOf(valor)` / `ultimo_indice_de` | `T` | `int` | Última posición o `-1`. |
| `sort()` / `ordenar` | — | `void` | Orden ascendente. |
| `reverse()` / `invertir` | — | `void` | Invierte el orden. |
| `clear()` / `limpiar` | — | `void` | Elimina todo. |
| `length()` / `longitud` | — | `int` | Número de elementos. |
| `isEmpty()` / `esta_vacio` | — | `bool` | `true` si está vacío. |

### Parámetros y valores de retorno

- Los métodos que modifican (`add`, `insert`, `set`, `remove`, `sort`,
  `reverse`, `clear`) devuelven `void`; se usan como sentencia.
- Los métodos de consulta (`get`, `first`, `last`, `contains`,
  `indexOf`, `length`, `isEmpty`) devuelven un valor y se pueden usar en
  expresiones.
- `remove` y `get` lanzan `NX11` si el índice no existe.
- `first`, `last` y `pop` lanzan `NX50` si el vector está vacío.

## 5. Ejemplo completo

```
#inject Vector;

Vector<int> numeros = [5, 1, 4, 2, 3]

Console.println(numeros.length())     // 5
Console.println(numeros.contains(3))  // true

numeros.sort()
Console.println(numeros)              // [1, 2, 3, 4, 5]

numeros.reverse()
Console.println(numeros)              // [5, 4, 3, 2, 1]

numeros.insert(2, 99)
Console.println(numeros)              // [5, 4, 99, 3, 2, 1]

numeros.remove(0)
Console.println(numeros)              // [4, 99, 3, 2, 1]

int ultimo = numeros.pop()
Console.println(ultimo)               // 1
```

## 6. Recorrido

```
Vector<string> productos = ["Arroz", "Azucar", "Aceite"]

foreach (p in productos) {
    Console.println(p)
}

foreach (string p, productos) {
    Console.println(p)
}

for i in 0 ... productos.length() {
    Console.println(productos[i])
}
```

## 7. Pasar un Vector a una función

Los vectores se pasan con **copia de salida**: la función puede
modificarlos y los cambios se conservan en el llamador.

```
#inject Vector;

void ordenar(Vector<int>: v) -> void {
    v.sort()
}

Vector<int> datos = [3, 1, 2]
ordenar(datos)
Console.println(datos)   // [1, 2, 3]
```

## 8. Ordenar manualmente (burbuja)

```
#inject Vector;

Vector<int> v = [64, 34, 25, 12, 22, 11, 90]
int n = v.length()
for i in 0 ... n {
    for j in 0 ... (n - i - 1) {
        if (v[j] > v[j + 1]) {
            int aux = v[j]
            v[j] = v[j + 1]
            v[j + 1] = aux
        }
    }
}
Console.println(v)
```

## 9. Errores comunes

| Error | Código | Solución |
|-------|--------|----------|
| Índice fuera de rango | `NX11` | Usar `0 ... v.length()` y comprobar el índice. |
| Operar sobre vector vacío | `NX50` | Comprobar `isEmpty()` antes de `pop`/`first`/`last`. |
| Mezclar tipos en el literal | `NX07` | Usar un solo tipo: `[1, 2, 3]`, no `[1, "dos"]`. |
| Usar un método inexistente | — | Consultar la tabla de métodos. |

## 10. Complejidad

| Operación | Coste |
|-----------|-------|
| `get` / `set` / `length` | O(1) |
| `add` / `pop` | O(1) amortizado |
| `insert` / `remove` | O(n) |
| `contains` / `indexOf` | O(n) |
| `sort` | O(n log n) |
| `reverse` | O(n) |
