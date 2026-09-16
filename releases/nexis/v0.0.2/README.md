# Nexis v0.0.2 — Producto completo (actualización)

**Componente:** nexis (producto completo) · **Fecha:** 2026-09-12 · **Tipo:** Actualización

Segunda versión del lenguaje Nexis como producto instalable. Incluye compilador, intérprete, documentación, tests y extensión de VS Code actualizados.

## Qué incluye esta versión

- **Compilador** `nexisc` v0.0.2 — binario CLI para Linux x86_64.
- **Intérprete** `nexisi` v0.0.2 — binario CLI para Linux x86_64 con modo archivo, `--bytecode`, `--debug` y `--repl`.
- **Documentación** v0.0.2 — documentación oficial del lenguaje actualizada con guía de instalación, librerías propias y catálogo de errores ampliado.
- **Tests** v0.0.2 — suite de tests del lenguaje.
- **Extensión** v0.0.2 — gramática TextMate realineada con la documentación, `fs"…"`, `#inject`, 20 snippets e icono propio.

## Instaladores

| Plataforma | Artefacto |
|---|---|
| **Debian/Ubuntu (x86_64)** | [nexis-v0.0.2-linux-x86_64.deb](nexis-v0.0.2-linux-x86_64.deb) — instala con `sudo dpkg -i`. |
| **Otras distros Linux (x86_64)** | [nexis-v0.0.2-linux-x86_64.tar.xz](nexis-v0.0.2-linux-x86_64.tar.xz) — trae `install.sh` y `uninstall.sh`. |
| **Windows (x86_64)** | [nexis-v0.0.2-windows-x86_64.exe](nexis-v0.0.2-windows-x86_64.exe) — instalador NSIS que instala en `%LOCALAPPDATA%\Nexis` y añade `bin\` al `PATH`. |
| **Debian/Ubuntu (aarch64)** | [nexis-v0.0.2-linux-aarch64.deb](nexis-v0.0.2-linux-aarch64.deb) — instala con `sudo dpkg -i`. |
| **Otras distros Linux (aarch64)** | [nexis-v0.0.2-linux-aarch64.tar.xz](nexis-v0.0.2-linux-aarch64.tar.xz) — trae `install.sh` y `uninstall.sh`. |
| **Windows (aarch64)** | [nexis-v0.0.2-windows-aarch64.exe](nexis-v0.0.2-windows-aarch64.exe) — instalador NSIS que instala en `%LOCALAPPDATA%\Nexis` y añade `bin\` al `PATH`. |

> **macOS:** el instalador `.pkg` debe generarse en un equipo Mac; aún no está publicado.

## Cambios respecto a la anterior (v0.0.1)

- Compilador e intérprete regenerados con la versión actualizada del script de build.
- Documentación ampliada: guía de instalación (`docs/installation.md`), librerías propias (`docs/language/modules/librerias_propias.md`) y catálogo de errores actualizado.
- Extensión de VS Code actualizada a v0.0.2: gramática realineada, snippets e icono propio.

## Limitaciones

- El compilador y el intérprete implementan tipos, operadores, `Console` e interpolación `fs"…"`.
- No incluye aún control de flujo, funciones, POO, `try/catch` ni módulos reales (ver `COMPATIBILIDAD.md` dentro de los instaladores).
- La extensión v0.0.2 incluida en el paquete universal es la versión actualizada con gramática corregida.

## Guía de instalación

Guía completa para Linux, Windows y macOS:

- [Guía de instalación de Nexis](../../../installer/README.md)

## Publicar una nueva versión

1. Crea `releases/nexis/<versión>/` y añade los instaladores como `nexis-<versión>-<plataforma>.<ext>`.
2. Añade un `README.md` describiendo qué incluye esa versión y qué soluciona respecto a la anterior.
3. Actualiza el [índice de releases](../README.md).
