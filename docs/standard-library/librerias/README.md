# Librerías estándar de Nexis

Las librerías estándar reúnen funciones reutilizables del lenguaje. Cada página documenta la API prevista; la implementación queda pendiente.

## Catálogo

| Librería | Propósito | Documentación |
|----------|-----------|---------------|
| `vector` | Arreglo dinámico | [Vector](vector.md) |
| `stack` | Pila LIFO | [Stack](stack.md) |
| `queue` | Cola FIFO | [Queue](queue.md) |
| `set` | Conjunto de valores únicos | [Set](set.md) |
| `map` | Claves y valores | [Map](map.md) |
| `linked_list` | Lista de nodos enlazados | [Linked List](linked_list.md) |
| `tree` | Árbol binario de búsqueda | [Tree](tree.md) |
| `graph` | Vértices y conexiones | [Graph](graph.md) |
| `trie` | Árbol de prefijos | [Trie](trie.md) |
| `math` | Operaciones matemáticas | [Math](math.md) |
| `string` | Manipulación de cadenas | [String](string.md) |
| `file` | Lectura y escritura de archivos | [File](file.md) |
| `time` | Fechas, horas y medición de duración | [Time](time.md) |
| `random` | Generación de valores aleatorios | [Random](random.md) |
| `graphics` | Dibujo y visualización | [Graphics](graphics.md) |
| `network` | Comunicación de red | [Network](network.md) |

## Importación

```
#inject math;
#inject string;
#inject vector;
#inject stack;
#inject queue;
#inject set;
#inject map;
#inject linked_list;
#inject tree;
#inject graph;
#inject trie;
```

Las directivas se colocan al inicio del archivo y cada librería se importa una sola vez.

## Convenciones

- Los nombres de las librerías usan `snake_case` cuando tienen más de una palabra.
- Las funciones reciben argumentos explícitos y devuelven valores del tipo indicado.
- Las operaciones que pueden fallar deben devolver un error o lanzar una excepción documentada.
- La API descrita aquí es la base para la implementación futura del lenguaje.
