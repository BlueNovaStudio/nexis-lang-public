# Changelog

Todos los cambios notables del repositorio público de **Nexis** se documentan en este archivo.

El formato sigue [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/). Este proyecto aún no cumple con [Versionado Semántico](https://semver.org/): durante el desarrollo previo a **Nexis V1.0.0** los cambios menores pueden incrementar el parche.

## [0.0.2] - 2026-09-10

### Añadido

- Documentación actualizada a `v0.0.2`:
  - Nueva guía de instalación del lenguaje (`docs/installation.md`).
  - Nueva documentación de librerías propias (`docs/language/modules/librerias_propias.md`).
  - Catálogo de errores `NXxx` ampliado (`docs/errores.md` y `docs/language/errors/errors.md`).
  - Índice y sección de tipos primitivos de la documentación actualizados.
- Tests actualizados: métodos de la librería estándar renombrados de español a inglés (`agregar` → `add`, `obtener` → `get`, `longitud` → `length`, `apilar` → `push`, `contiene` → `contains`, etc.).
- Compilador `nexisc` `v0.0.2` (actualización): binario regenerado para Linux x86_64 y aarch64 con paridad de versionado con el intérprete y el producto completo.
- Intérprete `nexisi` `v0.0.2` (actualización): binario regenerado para Linux x86_64 y aarch64 con paridad de versionado con el compilador y el producto completo.
- Producto completo `v0.0.2` (actualización): instaladores para Windows (`.exe` NSIS), Debian/Ubuntu (`.deb`) y otras distribuciones Linux (`.tar.xz`), en x86_64 y aarch64.
- Extensión de VS Code `v0.0.1`: artefacto actualizado y renombrado a `nexis-0.0.1.vsix` (reemplaza al viejo `nexis-programming-language-support-0.0.1.vsix`).

### Cambiado

- Extensión de Visual Studio Code actualizada a `v0.0.2` (replanteamiento completo de la gramática TextMate):
  - Gramática realineada con la documentación del lenguaje: keywords, tipos y operadores reales (`if/else`, `for`, `foreach`, `switch`, `func`, `void`, `emit ->`, `try/catch/finally`, `class`, `struct`…).
  - `#builtins` corregido e incluido (`Console.print/println/input`, `math.*`, `string.*`, `file.*`, `time.*`, `random.*`, `graphics.*`, `network.*`).
  - Soporte de cadenas interpoladas `fs"…"`, caracteres `'c'`, literales numéricos y las 5 formas de comentario.
  - Directiva `#inject`, funciones y tipos genéricos (`Vector<int>`).
  - 20 snippets, icono propio e identidad NEXIS, y manual interno `docs/extension/README.md`.
  - Se eliminan las keywords, tipos y operadores inventados que arrastraba `v0.0.1`.

## [0.0.1] - 2026-09-09

### Añadido

- Compilador `nexisc` `v0.0.1` (Release inicial): binario para Linux x86_64 que interpreta y ejecuta programas `.nxs`.
- Intérprete `nexisi` `v0.0.1` (Release inicial): binario para Linux x86_64 con modo archivo, `--bytecode`, `--debug` y `--repl`.
- Producto completo `v0.0.1` (demo): instaladores tipo aplicación para Windows (`.exe` NSIS), Debian/Ubuntu (`.deb`) y otras distribuciones Linux (`.tar.xz`), además del paquete universal `.zip` con binarios, documentación, tests y extensión.

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

- **Nexis V1.0.0** (versión final del producto): completar el alcance del lenguaje (control de flujo, funciones, POO, `try/catch` y módulos reales) en el compilador y el intérprete.
- Instalador de macOS (`.pkg`), que debe generarse en un equipo Mac.
