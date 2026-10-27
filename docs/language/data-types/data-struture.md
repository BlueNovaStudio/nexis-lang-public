# Estructuras de datos en Nexis

Nexis ofrece estructuras de datos genéricas declaradas con la forma `Estructura<T>`. Permiten almacenar y organizar colecciones de elementos del mismo tipo.

> La referencia completa de cada estructura está en la
> [API de colecciones de la referencia rápida](../../referencia-api.md#15-api-de-colecciones).
> Aquí tienes un resumen orientado al curso.

## Estructuras disponibles

| Estructura | Comportamiento | Declaración | Métodos clave |
|------------|----------------|-------------|---------------|
| `Vector<T>` | Arreglo dinámico | `Vector<int> nums = []` | `add`, `get`, `remove`, `sort` |
| `Stack<T>` | LIFO (pila) | `Stack<int> pila = Stack()` | `push`, `pop`, `peek` |
| `Queue<T>` | FIFO (cola) | `Queue<int> cola = Queue()` | `enqueue`, `dequeue`, `front` |
| `Set<T>` | Valores únicos | `Set<int> ids = {}` | `add`, `contains`, `remove` |
| `Map<K,V>` | Claves → valores | `Map<string,int> inv = {}` | `put`, `get`, `contains` |
| `LinkedList<T>` | Nodos enlazados | `LinkedList<int> lista = LinkedList()` | `addFirst`, `addLast` |
| `Tree<T>` | Árbol binario de búsqueda | `Tree<int> arbol = Tree()` | `insert`, `search`, `inOrder` |
| `Graph<T>` | Vértices y aristas | `Graph<string> grafo = Graph()` | `addNode`, `connect`, `neighbors` |
| `Trie` | Árbol de prefijos | `Trie dict = Trie()` | `insert`, `startsWith` |

## Literales

- `[]` inicializa un `Vector`.
- `{}` con dos puntos (`{clave: valor}`) inicializa un `Map`.
- `{}` sin dos puntos (`{10, 20}`) inicializa un `Set`.

```nexis
#inject Vector;
#inject Map;
#inject Set;

Vector<int> numeros = [1, 2, 3]
Map<string, int> inventario = {"manzanas": 3}
Set<int> activos = {1, 2, 3}
```

## Declaración con tipo explícito

En V0.0.6 **el tipo es obligatorio** al declarar una colección: no existe
inferencia con `:=`. Escribe siempre `Tipo nombre = ...`:

```nexis
Vector<int> numeros = [1, 2, 3]
Map<string, string> capitales = {"Peru": "Lima"}
Set<int> ids = {10, 15, 20}
```

Si se intenta `numeros := [1, 2, 3]`, el compilador responde con `NX02`
(variable no definida), porque no reconoce la declaración.

## Reglas importantes

1. Cada estructura requiere su importación: `#inject Vector;`, `#inject Stack;`, etc.
2. Todas son **tipadas**: `Vector<string>` no puede guardar enteros (NX07).
3. Los índices empiezan en **0**.
4. Operar sobre una estructura vacía produce NX50.

## Recorrido

Todas las estructuras iterables se recorren con `foreach`:

```nexis
foreach (numero in numeros) {
    Console.print(numero)
}
```

## Errores relacionados

- [NX11](../errors/catalog-01-variables-y-tipos.md#nx11-índice-fuera-de-rango): índice fuera de rango.
- [NX50](../errors/catalog-03-errores-y-colecciones.md#nx50-operación-sobre-colección-vacía): operar sobre una colección vacía.
- [NX51](../errors/catalog-03-errores-y-colecciones.md#nx51-modificar-colección-durante-iteración): modificar mientras se itera.

> La documentación completa de cada estructura está en la
> [API de colecciones de la referencia rápida](../../referencia-api.md#15-api-de-colecciones).
