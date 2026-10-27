# 📚 Documentación de Nexis V0.0.6

Nexis es un lenguaje de programación con tipado estático, colecciones
genéricas, structs, clases, plantillas y manejo de errores. Esta carpeta es la
**fuente única de documentación**: no hay copias duplicadas en otras rutas.

## Empieza aquí

| Quiero… | Documento |
|---------|-----------|
| Ver el lenguaje de principio a fin | [Recorrido del lenguaje](ejemplos/01-lenguaje.md) (continúa en [parte 2](ejemplos/06-lenguaje-avanzado.md)) |
| Aprender todas las colecciones | [Colecciones](ejemplos/02-colecciones.md) (continúa en [parte 2](ejemplos/08-colecciones-avanzado.md)) |
| Usar `math`, `string`, `file`, `random`, `time` | [Librerías estándar](ejemplos/03-librerias.md) |
| Implementar algoritmos clásicos | [Algoritmos](ejemplos/04-algoritmos.md) (continúa en [parte 2](ejemplos/07-algoritmos-avanzado.md)) |
| Construir un proyecto completo | [Proyectos](ejemplos/05-proyectos.md) |
| Buscar una firma o sintaxis | [Referencia rápida](referencia-rapida.md) + [Referencia API](referencia-api.md) |
| Resolver un error `NXxx` | [Catálogo de errores](language/errors/errors.md) |
| Instalar el compilador | [Instalación](installation.md) |
| Ejecutar la demo de la versión | [Demo V0.0.6](demo-v0.0.6.md) |
| Entender el código del compilador | [Arquitectura](arquitectura.md) |

Todos los ejemplos de los capítulos 01–08 se ejecutan y se comparan
automáticamente con su salida mediante `tests/run_doc_examples.ps1`.

---

## 1. Fundamentos del lenguaje

- [Tipos primitivos](language/data-types/primitive-types.md)
- [Estructuras de datos](language/data-types/data-struture.md)
- [Declaración de variables](language/variables/declaration.md)
- [Impresión y lectura](language/variables/input-output.md)
- [Operadores y precedencia](language/operators/operadores.md)
- [Comentarios](language/comments/comments.md)

## 2. Control de flujo

- [Condicionales: `if`, `else`, `switch`](language/control-flow/conditionals.md)
- [Bucles: `while`, `do while`, `for`, `foreach`](language/control-flow/loops.md)

## 3. Funciones y módulos

- [Guía completa de funciones](language/functions/funtions.md)
- [Funciones con retorno](language/functions/return-values.md)
- [Importación de librerías y archivos](language/modules/imports.md)
- [Crear librerías propias](language/modules/librerias_propias.md)

## 4. Programación orientada a objetos

- [Structs](language/poo/structs.md)
- [Clases, `init` y `self`](language/poo/classes.md)

## 5. Colecciones y librerías

### Estructuras de datos

| Estructura | Documento | Estado |
|------------|-----------|--------|
| `Vector<T>` | [Vector](standard-library/librerias/vector.md) | Implementada |
| `LinkedList<T>` | [Linked List](standard-library/librerias/linked_list.md) | Implementada |
| `Stack<T>` | [Stack](standard-library/librerias/stack.md) | Implementada |
| `Queue<T>` | [Queue](standard-library/librerias/queue.md) | Implementada |
| `Set<T>` | [Set](standard-library/librerias/set.md) | Implementada |
| `Map<K, V>` | [Map](standard-library/librerias/map.md) | Implementada |
| `Tree<T>` | [Tree](standard-library/librerias/tree.md) | Implementada |
| `Trie` | [Trie](standard-library/librerias/trie.md) | Implementada |
| `Graph<T>` | [Graph](standard-library/librerias/graph.md) | Implementada |

### Librerías nativas

| Librería | Propósito | Estado | Documento |
|----------|-----------|--------|-----------|
| `math` | Operaciones matemáticas | Parcial | [Math](standard-library/librerias/math.md) |
| `string` | Manipulación de cadenas | Parcial | [String](standard-library/librerias/string.md) |
| `file` | Lectura y escritura de archivos | Parcial | [File](standard-library/librerias/file.md) |
| `random` | Valores pseudoaleatorios | Parcial | [Random](standard-library/librerias/random.md) |
| `time` | Medición de duración | Parcial | [Time](standard-library/librerias/time.md) |
| `graphics` | Dibujo y visualización | Reservada | [Graphics](standard-library/librerias/graphics.md) |
| `network` | Comunicación de red | Reservada | [Network](standard-library/librerias/network.md) |

> **Parcial**: la librería funciona, pero su API aún no está completa.
> **Reservada**: las funciones están declaradas pero devuelven `void`.

Convenciones:

- Las colecciones se importan con `#inject Vector;`, `#inject Map;`, etc.
- Los métodos tienen alias en inglés y español (`add`/`agregar`).
- Las colecciones y los structs se pasan a funciones con **copia de salida**:
  los cambios vuelven al llamador.
- Consulta la [referencia rápida](referencia-rapida.md) para la tabla completa
  de métodos y firmas.

## 6. Errores y depuración

- [Catálogo completo de errores NX](language/errors/errors.md)
  - [NX00–NX19: variables y tipos](language/errors/catalog-01-variables-y-tipos.md)
  - [NX20–NX39: control de flujo y funciones](language/errors/catalog-02-control-y-funciones.md)
  - [NX40–NX59: errores y colecciones](language/errors/catalog-03-errores-y-colecciones.md)
  - [NX60–NX99: E/S, módulos, red y sistema](language/errors/catalog-04-io-modulos-y-sistema.md)
- [Try / catch / finally](language/errors/try_catch.md)
- [Guía rápida de errores](errores.md)

## 7. Ejemplos ejecutables

1. [Lenguaje, parte 1: tipos, operadores, control de flujo, funciones y plantillas](ejemplos/01-lenguaje.md)
2. [Lenguaje, parte 2: globales, structs, clases, errores, módulos e integrador](ejemplos/06-lenguaje-avanzado.md)
3. [Colecciones, parte 1: `Vector`, `LinkedList`, `Stack`, `Queue` y `Set`](ejemplos/02-colecciones.md)
4. [Colecciones, parte 2: `Map`, `Tree`, `Trie`, `Graph` y guía de elección](ejemplos/08-colecciones-avanzado.md)
5. [Librerías: math, string, file, random, time y Console](ejemplos/03-librerias.md)
6. [Algoritmos, parte 1: ordenamientos y búsquedas](ejemplos/04-algoritmos.md)
7. [Algoritmos, parte 2: recursión, matrices, cadenas y matemáticas](ejemplos/07-algoritmos-avanzado.md)
8. [Proyectos: inventario, agenda, análisis de texto, tareas y rutas](ejemplos/05-proyectos.md)

## 8. Referencia y mantenimiento

- [Referencia rápida: sintaxis del lenguaje](referencia-rapida.md)
- [Referencia API: colecciones y librerías](referencia-api.md)
- [Arquitectura del compilador y del intérprete](arquitectura.md)
- [Demo V0.0.6](demo-v0.0.6.md)
- [Instalación de `nexisc`](installation.md)

### Comandos de verificación

```powershell
cargo test --manifest-path compiler/Cargo.toml
powershell -ExecutionPolicy Bypass -File tests/run_tests.ps1
powershell -ExecutionPolicy Bypass -File tests/run_doc_examples.ps1
```

- `run_tests.ps1` ejecuta la suite de regresión (101 casos).
- `run_doc_examples.ps1` extrae y ejecuta todos los bloques `nexis` de
  `docs/ejemplos/*.md` y de `docs/referencia-rapida.md`, comparando la salida.
