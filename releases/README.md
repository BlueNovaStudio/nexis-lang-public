# 📦 Releases de Nexis

Este directorio guarda el **historial de versiones** de cada componente del proyecto.

El proyecto se organiza por componentes y, además, hay una carpeta especial para la **versión completa del lenguaje** (lo que un usuario instalaría).

## Componentes

| Componente | Qué es | Carpeta de releases |
|---|---|---|
| **nexis** | Producto completo del lenguaje (docs + tests + extension + compiler + interpreter) | [releases/nexis](nexis/README.md) |
| **docs** | Documentación oficial y tests del lenguaje | [releases/docs](docs/) |
| **extension** | Extensión de VS Code (sintaxis, comentarios y consola) | [releases/extension](extension/) |
| **compiler** | Compilador del lenguaje | [releases/compiler](compiler/README.md) |
| **interpreter** | Intérprete del lenguaje | [releases/interpreter](interpreter/README.md) |

## Releases publicadas

| Release | Componente | Fecha | Tipo | Artefacto | Changelog |
|---|---|---|---|---|---|
| v0.0.1 | docs | 2026-09-05 | Demo | [nexis-docs-v0.0.1.zip](docs/v0.0.1/nexis-docs-v0.0.1.zip) · [nexis-tests-v0.0.1.zip](docs/v0.0.1/nexis-tests-v0.0.1.zip) | [ver](docs/v0.0.1/README.md) |
| v0.0.1 | extension | 2026-09-05 | Release inicial | [nexis-programming-language-support-0.0.1.vsix](extension/v0.0.1/nexis-programming-language-support-0.0.1.vsix) | [ver](extension/v0.0.1/README.md) |

## Producto completo (Nexis)

La versión general del lenguaje (**Nexis V1.0.0**) aún **no existe**: requiere el compilador y el intérprete. El historial de estas versiones se guarda en [releases/nexis](nexis/README.md).

## Componentes sin releases

- [compiler](compiler/README.md) — aún sin versiones publicadas.
- [interpreter](interpreter/README.md) — aún sin versiones publicadas.

## Cómo añadir una nueva versión

1. Crea la carpeta `releases/<componente>/<versión>/`.
2. Sube el artefacto comprimido con el nombre de la versión:
   - docs → `nexis-docs-<versión>.zip` (y `nexis-tests-<versión>.zip` si aplica).
   - extension → `nexis-programming-language-support-<versión>.vsix`.
   - compiler/interpreter → `nexis-compiler-<versión>.zip` / `nexis-interpreter-<versión>.zip`.
   - nexis (producto completo) → `nexis-<versión>.zip`.
3. Añade un `README.md` en la carpeta de la versión describiendo qué incluye y qué soluciona o mejora respecto a la anterior.
4. Actualiza este índice añadiendo una fila a la tabla.