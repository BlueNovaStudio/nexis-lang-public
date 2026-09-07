# Changelog

Todos los cambios notables del repositorio público de **Nexis** se documentan en este archivo.

El formato sigue [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/). Este proyecto aún no cumple con [Versionado Semántico](https://semver.org/): durante el desarrollo previo a **Nexis V1.0.0** los cambios menores pueden incrementar el parche.

## [0.0.1] - 2026-09-05

### Añadido

- Documentación oficial del lenguaje (`docs/`):
  - Fundamentos: tipos de datos, variables, entrada/salida, operadores y comentarios.
  - Estructuras de control: condicionales y bucles.
  - Funciones, módulos e importación de librerías.
  - Estructuras de datos y librería estándar: `Vector`, `Stack`, `Queue`, `Set`, `Map`, `LinkedList`, `Tree`, `Graph` y `Trie`.
  - Programación orientada a objetos: structs, clases y objetos.
  - Errores y depuración: `try/catch` y catálogo completo de errores `NXxx`.
- Extensión de Visual Studio Code «Nexis Language Support by BlueNova»:
  - Resaltado de sintaxis del lenguaje (gramática TextMate `source.nexis`).
  - Soporte de comentarios y configuración del lenguaje.
  - Registro de archivos `.nxs`.
- Primeras releases (`releases/`):
  - `docs` v0.0.1 (Demo) — documentación y tests.
  - `extension` v0.0.1 (Release inicial) — paquete `.vsix`.

### Pendiente

- **Nexis V1.0.0** (producto completo): requiere el compilador y el intérprete.
- Instaladores completos del lenguaje.