# Instalador de Nexis

Este directorio contiene los **instaladores oficiales** del lenguaje Nexis para llevar el compilador y el intérprete a tu equipo.

## Estado actual

| Componente | Versión | Estado | Windows | Linux |
|---|---|---|---|---|
| Producto completo | v0.0.1 (demo) | Publicado | **[nexis-v0.0.1-windows-x86_64.exe](v0.0.1/nexis-v0.0.1-windows-x86_64.exe)** | **Debian/Ubuntu:** [nexis-v0.0.1-linux-x86_64.deb](v0.0.1/nexis-v0.0.1-linux-x86_64.deb) <br> **Otras distros:** [nexis-v0.0.1-linux-x86_64.tar.xz](v0.0.1/nexis-v0.0.1-linux-x86_64.tar.xz) |

> **macOS:** el instalador `.pkg` está pendiente (debe generarse en un equipo Mac).

## Qué incluye el instalador

- El **compilador** `nexisc` y el **intérprete** `nexisi` (v0.0.1).
- La **documentación** oficial y la **suite de tests** del lenguaje.
- La **extensión de VS Code** (`.vsix`).

> La versión `v0.0.1` es una **demo**: la implementación cubre tipos, operadores, `Console` e interpolación `fs"…"`. El alcance completo (control de flujo, funciones, POO, `try/catch` y módulos) llegará con **Nexis V1.0.0**.

## Extensiones de VS Code

### Última versión (v0.0.2 — recomendada)

Gramática realineada con la documentación, `fs"…"`, `#inject`, 20 snippets e icono propio:

1. Descarga [nexis-0.0.2.vsix](../releases/extension/v0.0.2/nexis-0.0.2.vsix).
2. En VS Code abre la paleta de comandos (`Ctrl+Shift+P`).
3. Ejecuta *Extensions: Install from VSIX...* y selecciona el archivo.

### Incluida en el instalador (v0.0.1)

El paquete universal del producto lleva `nexis-programming-language-support-0.0.1.vsix` (soporte base de sintaxis).

## Cómo instalar el producto

Descarga el instalador de la tabla de arriba según tu sistema:

- **Windows:** ejecuta el `.exe` y sigue el asistente.
- **Debian/Ubuntu:** `sudo dpkg -i nexis-v0.0.1-linux-x86_64.deb`.
- **Otras distros:** descomprime el `.tar.xz` y ejecuta `install.sh`.

Tras instalar, asegúrate de que los binarios `nexisc` y `nexisi` están en el `PATH`.

## Publicar una nueva versión

1. Genera los instaladores por plataforma (Linux y Windows; macOS cuando haya un Mac disponible).
2. Añade los artefactos a [releases/nexis/](../releases/nexis/README.md) como `nexis-<versión>-<plataforma>.<ext>`.
3. Actualiza la tabla de estado y el [índice de releases](../releases/README.md).