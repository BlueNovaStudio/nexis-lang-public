# 🗂️ Estructuras de datos en Nexis

Nexis ofrece estructuras de datos genéricas declaradas con la forma `Estructura<T>`. Permiten almacenar y organizar colecciones de elementos del mismo tipo.

> La referencia completa de cada estructura está en [standard-library/collections](../../standard-library/collections/README.md). Aquí tienes un resumen orientado al curso.

## Estructuras disponibles

| Estructura | Comportamiento | Declaración | Métodos clave |
|------------|----------------|-------------|---------------|
| `Vector<T>` | Arreglo dinámico | `Vector<int> nums = []` | `agregar`, `obtener`, `eliminar`, `ordenar` |
| `Stack<T>` | LIFO (pila) | `Stack<int> pila = Stack()` | `apilar`, `desapilar`, `cima` |
| `Queue<T>` | FIFO (cola) | `Queue<int> cola = Queue()` | `encolar`, `desencolar`, `frente` |
| `Set<T>` | Valores únicos | `Set<int> ids = {}` | `agregar`, `contiene`, `eliminar` |
| `Map<K,V>` | Claves → valores | `Map<string,int> inv = {}` | `poner`, `obtener`, `contiene` |
| `LinkedList<T>` | Nodos enlazados | `LinkedList<int> lista = LinkedList()` | `agregar_frente`, `agregar_fondo` |
| `Tree<T>` | Árbol binario de búsqueda | `Tree<int> arbol = Tree()` | `insertar`, `buscar`, `en_orden` |
| `Graph<T>` | Vértices y aristas | `Graph<string> grafo = Graph()` | `agregar_nodo`, `conectar`, `adyacentes` |
| `Trie` | Árbol de prefijos | `Trie dict = Trie()` | `insertar`, `comienza_con` |

## Literales

- `[]` inicializa un `Vector`.
- `{}` con dos puntos (`{clave: valor}`) inicializa un `Map`.
- `{}` sin dos puntos (`{10, 20}`) inicializa un `Set`.

```nexis
#inject vector;
#inject map;
#inject set;

Vector<int> numeros = [1, 2, 3]
Map<string, int> inventario = {"manzanas": 3}
Set<int> activos = {1, 2, 3}
```

## Inferencia con `:=`

Cuando la inicialización permite deducir el tipo, se puede usar `:=`:

```nexis
numeros := [1, 2, 3]
capitales := {"Peru": "Lima"}
ids := {10, 15, 20}
```

## Reglas importantes

1. Cada estructura requiere su importación: `#inject vector;`, `#inject stack;`, etc.
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

- [NX11](../errors/errors.md#nx11-índice-fuera-de-rango): índice fuera de rango.
- [NX50](../errors/errors.md#nx50-operación-sobre-colección-vacía): operar sobre una colección vacía.
- [NX51](../errors/errors.md#nx51-modificar-colección-durante-iteración): modificar mientras se itera.

> La documentación completa de cada estructura está en [standard-library/collections](../../standard-library/collections/README.md).