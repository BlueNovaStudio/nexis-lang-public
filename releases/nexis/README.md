# Nexis — Producto completo

Esta carpeta guarda las **versiones del lenguaje Nexis como producto completo** (el «todo»): la versión que un usuario normal buscaría instalar, que agrupa:

- Documentación y tests (`docs/`)
- Extensión de VS Code (`releases/extension/`)
- Compilador (`nexisc`) e intérprete (`nexisi`)

## Estado

| Versión | Estado |
|---|---|
| **v0.0.1** (demo) | ✅ Publicada — instaladores para Windows (`.exe`) y Linux (`.deb`, `.tar.xz`) más el paquete universal `.zip` |
| **V1.0.0** | ⏳ Pendiente — requiere el alcance completo del lenguaje (control de flujo, funciones, POO, `try/catch` y módulos reales) y el instalador de macOS |

## v0.0.1 — Producto completo (demo)

Primera versión del lenguaje como producto instalable. Publicada el **2026-09-09**.

### Instaladores

| Plataforma | Artefacto |
|---|---|
| **Windows** | [nexis-v0.0.1-windows-x86_64.exe](v0.0.1/nexis-v0.0.1-windows-x86_64.exe) — instalador NSIS que instala en `%LOCALAPPDATA%\Nexis` y añade `bin\` al `PATH`. |
| **Debian/Ubuntu** | [nexis-v0.0.1-linux-x86_64.deb](v0.0.1/nexis-v0.0.1-linux-x86_64.deb) — instala con `sudo dpkg -i`. |
| **Otras distros Linux** | [nexis-v0.0.1-linux-x86_64.tar.xz](v0.0.1/nexis-v0.0.1-linux-x86_64.tar.xz) — trae `install.sh` y `uninstall.sh`. |
| **Universal** | [nexis-v0.0.1-linux-x86_64.zip](v0.0.1/nexis-v0.0.1-linux-x86_64.zip) — binarios `nexisc`/`nexisi` + documentación + tests + extensión de VS Code. |

> **macOS:** el instalador `.pkg` debe generarse en un equipo Mac; aún no está publicado.

### Contenido del paquete universal

- Binarios: `bin/nexisc` (compilador) y `bin/nexisi` (intérprete), ambos en su versión `v0.0.1`.
- Documentación completa del lenguaje (`docs/`).
- Suite de tests del lenguaje (`tests/`).
- Extensión de VS Code (`nexis-programming-language-support-0.0.1.vsix`).

### Limitaciones de la demo v0.0.1

- El compilador y el intérprete implementan tipos, operadores, `Console` e interpolación `fs"…"`.
- No incluye aún control de flujo, funciones, POO, `try/catch` ni módulos reales (ver `COMPATIBILIDAD.md` dentro de los instaladores).

## Publicar una nueva versión

1. Crea `releases/nexis/<versión>/` y añade los instaladores como `nexis-<versión>-<plataforma>.<ext>`.
2. Añade un `README.md` describiendo qué incluye esa versión y qué soluciona respecto a la anterior.
3. Actualiza el [índice de releases](../README.md).