# 📚 Referencia API: colecciones y librerías

Continuación de [referencia-rapida.md](referencia-rapida.md): tablas completas de la
API de las 9 colecciones, de las librerías estándar y las secciones finales de
errores y ejemplos. La parte 1 cubre la sintaxis del lenguaje (secciones 1 a 14).

---

## 15. API de colecciones

Todas las colecciones se importan con `#inject Nombre;` y aceptan nombres en
inglés y español.

### `Vector<T>`

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `add` / `agregar` | `T` | `void` | Añade al final. |
| `insert` / `insertar` | `int`, `T` | `void` | Inserta en la posición. |
| `get` / `obtener` | `int` | `T` | Lee por índice. |
| `set` / `asignar` | `int`, `T` | `void` | Modifica por índice. |
| `remove` / `eliminar` | `int` | `void` | Elimina y desplaza. |
| `pop` / `extraer` | — | `T` | Quita y devuelve el último. |
| `first` / `primero` | — | `T` | Primer elemento. |
| `last` / `ultimo` | — | `T` | Último elemento. |
| `contains` / `contiene` | `T` | `bool` | Comprueba existencia. |
| `indexOf` / `indice_de` | `T` | `int` | Primera posición o `-1`. |
| `lastIndexOf` / `ultimo_indice_de` | `T` | `int` | Última posición o `-1`. |
| `sort` / `ordenar` | — | `void` | Orden ascendente. |
| `reverse` / `invertir` | — | `void` | Invierte. |
| `clear` / `limpiar` | — | `void` | Vacía. |
| `length` / `longitud` | — | `int` | Número de elementos. |
| `isEmpty` / `esta_vacio` | — | `bool` | ¿Está vacío? |

Además: `v[i]` para leer y `v[i] = x` para escribir.

### `LinkedList<T>`

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `add` / `agregar` | `T` | `void` | Añade al final. |
| `addFirst` / `agregar_frente` | `T` | `void` | Añade al inicio. |
| `addLast` / `agregar_fondo` | `T` | `void` | Añade al final. |
| `removeFirst` / `eliminar_frente` | — | `T` | Quita y devuelve el primero. |
| `removeLast` / `eliminar_fondo` | — | `T` | Quita y devuelve el último. |
| `remove` / `eliminar` | `int` | `void` | Elimina por índice. |
| `get` / `obtener` | `int` | `T` | Lee por índice. |
| `set` / `asignar` | `int`, `T` | `void` | Modifica por índice. |
| `first` / `primero` | — | `T` | Primer elemento. |
| `last` / `ultimo` | — | `T` | Último elemento. |
| `contains` / `contiene` | `T` | `bool` | Comprueba existencia. |
| `indexOf` / `indice_de` | `T` | `int` | Posición o `-1`. |
| `sort` / `ordenar` | — | `void` | Orden ascendente. |
| `reverse` / `invertir` | — | `void` | Invierte. |
| `length` / `longitud` | — | `int` | Número de elementos. |
| `isEmpty` / `esta_vacio` | — | `bool` | ¿Está vacía? |

### `Stack<T>`

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `push` / `apilar` | `T` | `void` | Apila en la cima. |
| `pop` / `desapilar` | — | `T` | Quita y devuelve la cima. |
| `peek` / `top` / `cima` | — | `T` | Consulta la cima. |
| `get` / `obtener` | `int` | `T` | Lee por índice (0 = fondo). |
| `sort` / `ordenar` | — | `void` | Ordena de fondo a cima. |
| `reverse` / `invertir` | — | `void` | Invierte. |
| `length` / `longitud` | — | `int` | Número de elementos. |
| `isEmpty` / `esta_vacio` | — | `bool` | ¿Está vacía? |

### `Queue<T>`

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `enqueue` / `encolar` | `T` | `void` | Añade al final. |
| `dequeue` / `desencolar` | — | `T` | Quita y devuelve el frente. |
| `front` / `peek` / `frente` | — | `T` | Consulta el frente. |
| `get` / `obtener` | `int` | `T` | Lee por índice. |
| `sort` / `ordenar` | — | `void` | Ordena de frente a final. |
| `reverse` / `invertir` | — | `void` | Invierte. |
| `length` / `longitud` | — | `int` | Número de elementos. |
| `isEmpty` / `esta_vacio` | — | `bool` | ¿Está vacía? |

### `Set<T>`

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `add` / `agregar` | `T` | `void` | Añade si no existe. |
| `remove` / `eliminar` | `T` | `void` | Elimina si existe. |
| `contains` / `contiene` | `T` | `bool` | Comprueba pertenencia. |
| `length` / `longitud` | — | `int` | Número de elementos. |
| `isEmpty` / `esta_vacio` | — | `bool` | ¿Está vacío? |

`s[i]` devuelve el i-ésimo elemento en **orden ascendente**.

### `Map<K, V>`

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `put` / `set` / `poner` | `K`, `V` | `void` | Crea o actualiza. |
| `get` / `obtener` | `K` | `V` | Devuelve el valor; `NX52` si no existe. |
| `contains` / `contiene` | `K` | `bool` | ¿Existe la clave? |
| `remove` / `eliminar` | `K` | `void` | Elimina la pareja. |
| `keys` / `claves` | — | `Vector<K>` | Todas las claves. |
| `values` / `valores` | — | `Vector<V>` | Todos los valores. |
| `length` / `longitud` | — | `int` | Número de parejas. |
| `isEmpty` / `esta_vacio` | — | `bool` | ¿Está vacío? |

`foreach (clave in mapa)` entrega las claves. **El orden no está garantizado.**

### `Tree<T>`

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `insert` / `insertar` | `T` | `void` | Inserta manteniendo el orden. |
| `search` / `contains` / `buscar` / `contiene` | `T` | `bool` | ¿Existe? |
| `remove` / `eliminar` | `T` | `void` | Elimina si existe. |
| `inOrder` / `en_orden` | — | `void` | Imprime en orden ascendente. |
| `length` / `longitud` | — | `int` | Número de elementos. |
| `isEmpty` / `esta_vacio` | — | `bool` | ¿Está vacío? |

`t[i]` y `foreach` recorren en **orden ascendente**.

### `Trie`

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `insert` / `insertar` | `string` | `void` | Guarda una palabra. |
| `contains` / `contiene` | `string` | `bool` | ¿Existe la palabra completa? |
| `startsWith` / `comienza_con` | `string` | `bool` | ¿Alguna palabra empieza por el prefijo? |
| `searchPrefix` / `buscar_prefijo` | `string` | `Vector<string>` | Palabras con ese prefijo. |

### `Graph<T>`

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `addNode` / `agregar_nodo` | `T` | `void` | Añade un vértice. |
| `connect` / `addEdge` / `conectar` | `T`, `T`, `number` | `void` | Arista dirigida con peso. |
| `disconnect` / `removeEdge` / `desconectar` | `T`, `T` | `void` | Elimina la arista. |
| `neighbors` / `adjacent` / `adyacentes` | `T` | `Vector<T>` | Vecinos del nodo. |
| `breadthFirst` / `bfs` / `recorrido_anchura` | `T` | `void` | BFS (imprime). |
| `depthFirst` / `dfs` / `recorrido_profundidad` | `T` | `void` | DFS (imprime). |
| `length` / `longitud` | — | `int` | Número de nodos. |
| `isEmpty` / `esta_vacio` | — | `bool` | ¿Está vacío? |

Las aristas son **dirigidas**. Para una conexión bidireccional, llama a
`connect` en ambos sentidos.

---

## 16. API de librerías

### `math`

| Miembro | Parámetros | Devuelve |
|---------|------------|----------|
| `math.PI` | — | `double` |
| `math.E` | — | `double` |
| `sqrt(x)` | numérico | `double` |
| `pow(base, exp)` | numérico, numérico | `double` |
| `log(x)` | numérico | `double` (natural) |
| `abs(x)` | numérico | `double` |
| `floor(x)` | numérico | `double` |
| `ceil(x)` | numérico | `double` |
| `round(x)` | numérico | `double` |
| `min(a, b)` | numérico, numérico | `double` |
| `max(a, b)` | numérico, numérico | `double` |

Reservadas (no implementadas): `sin`, `cos`, `tan`, `asin`, `acos`, `atan`,
`log10`, `log2`, `trunc`.

### `string`

| Función | Parámetros | Devuelve |
|---------|------------|----------|
| `length` / `longitud` | `string` | `int` |
| `lowercase` / `minusculas` | `string` | `string` |
| `uppercase` / `mayusculas` | `string` | `string` |
| `trim` / `recortar` | `string` | `string` |
| `split` / `dividir` | `string`, `string` | `Vector<string>` |
| `contains` / `contiene` | `string`, `string` | `bool` |
| `startsWith` / `comienza_con` | `string`, `string` | `bool` |

### `file`

| Función | Parámetros | Devuelve |
|---------|------------|----------|
| `exists` / `existe` | `string` | `bool` |
| `read` / `leer` | `string` | `string` |
| `write` / `escribir` | `string`, `string` | `void` |

`read` lanza `ErrorArchivo` (`NX61`) si no existe. `write` sobrescribe y lanza
`ErrorArchivo` (`NX62`) si no puede escribir.

### `random`

| Función | Parámetros | Devuelve |
|---------|------------|----------|
| `integer` / `entero` | `int`, `int` | `int` en `[min, max]` |

### `time`

| Función | Parámetros | Devuelve |
|---------|------------|----------|
| `clock` / `reloj` | — | `int` (ms desde el inicio) |

### Reservadas

`graphics` y `network` están declaradas pero **no implementadas** en V0.0.6.

---

## 17. Códigos de error más frecuentes

| Código | Significado |
|--------|-------------|
| `NX01` | División por cero. |
| `NX02` | Variable no definida. |
| `NX03` | Reasignación de constante. |
| `NX04` | Declaración duplicada. |
| `NX07` | Tipo incompatible en asignación. |
| `NX10` | Operandos incompatibles. |
| `NX11` | Índice fuera de rango. |
| `NX12` | Conversión inválida. |
| `NX23` | Condición no booleana. |
| `NX32` | Número de argumentos incorrecto. |
| `NX33` | Tipo de argumento incorrecto. |
| `NX36` | `emit` en función `void`. |
| `NX42` | Error no capturado. |
| `NX50` | Operación sobre colección vacía. |
| `NX52` | Clave no encontrada en `Map`. |
| `NX60` | Formato de entrada inválido. |
| `NX61` | Archivo no encontrado. |
| `NX80` | Módulo no encontrado. |
| `NX82` | Función usada sin importar. |
| `NX90` | Error de sintaxis. |

Catálogo completo: [errors.md](language/errors/errors.md).

---

## 18. Errores comunes y solución

| Síntoma | Causa | Solución |
|---------|-------|----------|
| `NX82` | Usar `math`, `string`, `Vector`… sin `#inject`. | Añade el `#inject` al inicio del archivo. |
| `NX07` al concatenar | `"texto" + 42` | Usa `string(42)` o `fs"..."`. |
| `NX23` | `if (5)` | La condición debe ser `bool`: `if (x > 0)`. |
| `NX50` | `pop()`/`first()` en colección vacía. | Comprueba `isEmpty()` antes. |
| `NX11` | Índice igual a `length()`. | Usa `for i in 0 ... v.length()`. |
| `NX36` | `emit` en función `void`. | Quita el `emit` o cambia el retorno. |
| Bucle descendente vacío | `for i in 5 .. 0`. | Añade `step -1`. |
| `Map`/`Set` en orden variable | Iteración no ordenada. | Ordena `keys()` antes de imprimir. |
| No se puede asignar `lista[i].campo` | Asignación sobre índice. | Copia el struct, muta y reasigna. |
| `fs"..."` con `\n` literal | La interpolación no procesa escapes. | Concatena con `"\n"`. |

---

## 19. Ejemplos por tema

| Tema | Documento |
|------|-----------|
| Lenguaje, parte 1 (básico) | [01-lenguaje.md](ejemplos/01-lenguaje.md) |
| Lenguaje, parte 2 (avanzado) | [06-lenguaje-avanzado.md](ejemplos/06-lenguaje-avanzado.md) |
| Colecciones, parte 1 | [02-colecciones.md](ejemplos/02-colecciones.md) |
| Colecciones, parte 2 | [08-colecciones-avanzado.md](ejemplos/08-colecciones-avanzado.md) |
| Librerías estándar | [03-librerias.md](ejemplos/03-librerias.md) |
| Algoritmos, parte 1 | [04-algoritmos.md](ejemplos/04-algoritmos.md) |
| Algoritmos, parte 2 | [07-algoritmos-avanzado.md](ejemplos/07-algoritmos-avanzado.md) |
| Proyectos completos | [05-proyectos.md](ejemplos/05-proyectos.md) |
| Instalación | [installation.md](installation.md) |
| Demo V0.0.6 | [demo-v0.0.6.md](demo-v0.0.6.md) |
| Errores | [errores.md](errores.md) |

---

## 20. Comprobación rápida de sintaxis

```nexis
#inject Vector;
#inject Map;
#inject string;
#inject math;

struct Punto {
    int x;
    int y;
}

func distancia(Punto: a, Punto: b) -> double {
    int dx = b.x - a.x
    int dy = b.y - a.y
    emit -> math.sqrt(dx * dx + dy * dy)
}

Vector<Punto> puntos = [Punto(0, 0), Punto(3, 4)]
Map<string, int> edades = {"Ana": 20}

foreach (Punto p, puntos) {
    Console.println(fs"({p.x}, {p.y})")
}

Console.println(distancia(puntos[0], puntos[1]))
Console.println(edades.get("Ana"))
Console.println(string.uppercase("nexis"))
```

Salida:

```
(0, 0)
(3, 4)
5
20
NEXIS
```