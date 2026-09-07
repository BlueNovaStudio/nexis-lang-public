# Estructuras de datos en Nexis

Las estructuras de datos de Nexis usan tipos genéricos con la forma `Estructura<T>`. Los literales `[]` y `{}` permiten inicializar vectores, conjuntos y mapas de forma directa.

## Estructuras disponibles

| Estructura | Declaración | Documentación |
|------------|-------------|---------------|
| Vector | `Vector<T> valores = []` | [Vector](vector.md) |
| Pila | `Stack<T> historial = Stack()` | [Stack](stack.md) |
| Cola | `Queue<T> turnos = Queue()` | [Queue](queue.md) |
| Conjunto | `Set<T> valores = {}` | [Set](set.md) |
| Mapa | `Map<K, V> datos = {clave: valor}` | [Map](map.md) |
| Lista enlazada | `LinkedList<T> valores = LinkedList()` | [Linked List](linked_list.md) |
| Árbol | `Tree<T> valores = Tree()` | [Tree](tree.md) |
| Trie | `Trie diccionario = Trie()` | [Trie](trie.md) |
| Grafo | `Graph<T> red = Graph()` | [Graph](graph.md) |

## Inferencia de tipos

Cuando la inicialización permite deducir el tipo, se puede usar `:=`:

```
numeros := [1, 2, 3]
capitales := {"Peru": "Lima"}
ids := {10, 15, 20}
```

Las llaves con `:` representan un mapa; las llaves sin `:` representan un conjunto.