# Docs v0.0.2 — Actualización

**Componente:** docs · **Fecha:** 2026-09-12 · **Tipo:** Actualización

Segunda versión de la documentación oficial del lenguaje de programación **Nexis** y su batería de tests.

## Qué incluye esta versión

- **Documentación** (`docs`):
  - Fundamentos: tipos de datos, variables, entrada/salida, operadores y comentarios.
  - Estructuras de control: condicionales y bucles.
  - Funciones, módulos e importación de librerías (incluye guía de librerías propias).
  - Estructuras de datos y librería estándar: Vector, Stack, Queue, Set, Map, Linked List, Tree, Graph y Trie.
  - Programación orientada a objetos: structs, clases y objetos.
  - Errores y depuración: manejo de errores, try/catch y catálogo completo de errores NX (`NXxx`) ampliado.
  - Guía de instalación del lenguaje (`installation.md`).
  - Bloques de `examples`, `spec` y `reference`.
- **Tests** (`tests`): guías y casos de uso en 9 bloques: variables, condicionales, bucles, funciones, errores, estructuras, librerías, módulos e integrador.

## Artefactos

- [nexis-docs-v0.0.2.zip](nexis-docs-v0.0.2.zip) — snapshot completo de `docs/`.
- [nexis-tests-v0.0.2.zip](nexis-tests-v0.0.2.zip) — snapshot completo de `tests/`.

## Cambios respecto a la anterior (v0.0.1)

- **Nuevo:** `docs/installation.md` — guía de instalación del lenguaje paso a paso.
- **Nuevo:** `docs/language/modules/librerias_propias.md` — documentación sobre cómo crear librerías propias.
- **Ampliado:** `docs/errores.md` y `docs/language/errors/errors.md` — catálogo de errores NX actualizado y ampliado.
- **Actualizado:** `docs/README.md` — índice principal de la documentación.
- **Actualizado:** `docs/language/data-types/primitive-types.md` — tipos primitivos documentados con más detalle.
- **Actualizado:** `docs/language/errors/README.md` — introducción a la sección de errores mejorada.
- Varios archivos de `standard-library/` y `language/` con mejoras menores de formato y contenido.
- **Tests actualizados:** métodos de la librería estándar renombrados de español a inglés (`agregar` → `add`, `obtener` → `get`, `longitud` → `length`, `apilar` → `push`, `contiene` → `contains`, `insertar` → `insert`, `eliminar` → `remove`, etc.).

## Referencias

- [Documentación de Nexis](../../../docs/README.md)
- [Ejemplos de código](../../../examples/README.md)
