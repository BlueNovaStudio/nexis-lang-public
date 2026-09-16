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


### Compilador

| Release | Fecha | Tipo | Artefacto | Changelog |
|---|---|---|---|---|
| v0.0.1 | 2026-09-09 | Demo | [nexisc-v0.0.1-x86_64.zip](compiler/v0.0.1/nexisc-v0.0.1-x86_64.zip) | [ver](compiler/v0.0.1/README.md) |
| v0.0.2 | 2026-09-12 | Demo | [x86_64](compiler/v0.0.2/nexisc-v0.0.2-x86_64.zip) · [aarch64](compiler/v0.0.2/nexisc-v0.0.2-aarch64.zip) | [ver](compiler/v0.0.2/README.md) |

### Intérprete

| Release | Fecha | Tipo | Artefacto | Changelog |
|---|---|---|---|---|
| v0.0.1 | 2026-09-09 | Demo | [nexisi-v0.0.1-x86_64.zip](interpreter/v0.0.1/nexisi-v0.0.1-x86_64.zip) | [ver](interpreter/v0.0.1/README.md) |
| v0.0.2 | 2026-09-12 | Demo | [x86_64](interpreter/v0.0.2/nexisi-v0.0.2-x86_64.zip) · [aarch64](interpreter/v0.0.2/nexisi-v0.0.2-aarch64.zip) | [ver](interpreter/v0.0.2/README.md) |

### Extensión VS Code

| Release | Fecha | Tipo | Artefacto | Changelog |
|---|---|---|---|---|
| v0.0.1 | 2026-09-05 | Demo | [nexis-0.0.1.vsix](extension/v0.0.1/nexis-0.0.1.vsix) | [ver](extension/v0.0.1/README.md) |
| v0.0.2 | 2026-09-10 | Demo | [nexis-0.0.2.vsix](extension/v0.0.2/nexis-0.0.2.vsix) | [ver](extension/v0.0.2/README.md) |

### Documentación y tests

| Release | Fecha | Tipo | Artefacto | Changelog |
|---|---|---|---|---|
| v0.0.1 | 2026-09-05 | Demo | [nexis-docs-v0.0.1.zip](docs/v0.0.1/nexis-docs-v0.0.1.zip) · [nexis-tests-v0.0.1.zip](docs/v0.0.1/nexis-tests-v0.0.1.zip) | [ver](docs/v0.0.1/README.md) |
| v0.0.2 | 2026-09-12 | Demo | [nexis-docs-v0.0.2.zip](docs/v0.0.2/nexis-docs-v0.0.2.zip) · [nexis-tests-v0.0.2.zip](docs/v0.0.2/nexis-tests-v0.0.2.zip) | [ver](docs/v0.0.2/README.md) |

### Producto completo

| Release | Fecha | Tipo | Artefacto | Changelog |
|---|---|---|---|---|
| v0.0.1 | 2026-09-09 | Demo | [.deb](nexis/v0.0.1/nexis-v0.0.1-linux-x86_64.deb) · [.tar.xz](nexis/v0.0.1/nexis-v0.0.1-linux-x86_64.tar.xz) · [.exe](nexis/v0.0.1/nexis-v0.0.1-windows-x86_64.exe) · [.zip](nexis/v0.0.1/nexis-v0.0.1-linux-x86_64.zip) | [ver](nexis/README.md) |
| v0.0.2 | 2026-09-12 | Demo | [x86_64: .deb](nexis/v0.0.2/nexis-v0.0.2-linux-x86_64.deb) · [.tar.xz](nexis/v0.0.2/nexis-v0.0.2-linux-x86_64.tar.xz) · [.exe](nexis/v0.0.2/nexis-v0.0.2-windows-x86_64.exe) <br> [aarch64: .deb](nexis/v0.0.2/nexis-v0.0.2-linux-aarch64.deb) · [.tar.xz](nexis/v0.0.2/nexis-v0.0.2-linux-aarch64.tar.xz) · [.exe](nexis/v0.0.2/nexis-v0.0.2-windows-aarch64.exe) | [ver](nexis/README.md) |

## Producto completo (Nexis)

La versión **demo** del producto completo (**Nexis `v0.0.1` y `v0.0.2`**) ya está disponible con instaladores para Windows y Linux en [releases/nexis](nexis/README.md). La versión final **Nexis V1.0.0** sigue en desarrollo.

## Cómo añadir una nueva versión

1. Crea la carpeta `releases/<componente>/<versión>/`.
2. Sube el artefacto comprimido con el nombre de la versión:
   - docs → `nexis-docs-<versión>.zip` (y `nexis-tests-<versión>.zip` si aplica).
   - extension → `nexis-<versión>.vsix`.
   - compiler/interpreter → `nexisc-<versión>-<plataforma>.zip` / `nexisi-<versión>-<plataforma>.zip`.
   - nexis (producto completo) → instaladores `nexis-<versión>-<plataforma>.<ext>` (`.deb`, `.tar.xz`, `.exe`) y el paquete universal `nexis-<versión>.zip`.
3. Añade un `README.md` en la carpeta de la versión describiendo qué incluye y qué soluciona o mejora respecto a la anterior.
4. Actualiza este índice añadiendo una fila a la tabla.