# Nexis v0.0.1 — Producto completo (demo)

**Componente:** nexis · **Fecha:** 2026-09-09 · **Tipo:** Demo

Primera versión del **producto completo** de Nexis: instaladores tipo aplicación que llevan el compilador, el intérprete, la documentación, los tests y la extensión de VS Code a tu equipo.

## Qué incluye esta versión

- **Instalador de Windows** (`.exe`, NSIS): instala en `%LOCALAPPDATA%\Nexis` y añade `bin\` al `PATH`.
- **Instalador de Debian/Ubuntu** (`.deb`) y **de otras distros Linux** (`.tar.xz` con `install.sh`/`uninstall.sh`).
- **Paquete universal** (`.zip`): binarios `nexisc`/`nexisi` + documentación + tests + extensión de VS Code.
- Compilador `nexisc` v0.0.1 e intérprete `nexisi` v0.0.1, que comparten frontend y producen las mismas salidas y errores.

## Qué soluciona o aporta esta versión

- Primer modo de instalación «un solo clic» del lenguaje en Windows y Linux.
- Incluye la documentación oficial completa y la batería de tests en 9 bloques.
- Extensión de VS Code para resaltado de sintaxis (v0.0.1 dentro del paquete).

## Limitaciones (demo)

- Alcance de implementación limitado: tipos, operadores, `Console` e interpolación `fs"…"`.
- El control de flujo, las funciones, la POO, `try/catch` y los módulos reales llegan en **Nexis V1.0.0**.
- Sin instalador de macOS (`.pkg`): debe generarse en un equipo Mac.

## Artefactos

- [nexis-v0.0.1-windows-x86_64.exe](nexis-v0.0.1-windows-x86_64.exe)
- [nexis-v0.0.1-linux-x86_64.deb](nexis-v0.0.1-linux-x86_64.deb)
- [nexis-v0.0.1-linux-x86_64.tar.xz](nexis-v0.0.1-linux-x86_64.tar.xz)
- [nexis-v0.0.1-linux-x86_64.zip](nexis-v0.0.1-linux-x86_64.zip)

> Ver también el detalle en [releases/nexis](../README.md).