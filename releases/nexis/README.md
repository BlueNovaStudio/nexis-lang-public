# Nexis — Producto completo

Esta carpeta guarda las **versiones del lenguaje Nexis como producto completo** (el «todo»): la versión que un usuario normal buscaría instalar, que agrupa:

- Documentación y tests (`docs/`)
- Extensión de VS Code (`releases/extension/`)
- Compilador (`nexisc`) e intérprete (`nexisi`).
  > A partir de `v0.0.6` ambos vienen juntos dentro de un único ejecutable unificado: `nexis` (`nexis build`, `nexis run`).

## Estado

| Versión | Estado |
|---|---|
| **v0.0.6** | ✅ Publicada (demo) — ejecutable unificado `nexis` (Linux x86_64 y Windows `.exe`) |
| **v0.0.5** | ✅ Publicada (demo) — primer ejecutable unificado `nexis` (Linux x86_64 y Windows `.exe`) |
| **v0.0.4** | ✅ Publicada (demo) — instaladores `.deb`, `.tar.xz` y `.exe` |
| **v0.0.3** | ✅ Publicada (demo) — instaladores `.deb` y `.tar.xz` |
| **v0.0.2** | ✅ Publicada — instaladores para Windows (`.exe`) y Linux (`.deb`, `.tar.xz`), en x86_64 y aarch64 |
| **v0.0.1** (demo) | ✅ Publicada — instaladores para Windows (`.exe`) y Linux (`.deb`, `.tar.xz`) más el paquete universal `.zip` |
| **V1.0.0** | ⏳ Pendiente — requiere el alcance completo del lenguaje (control de flujo, funciones, POO, `try/catch` y módulos reales) y el instalador de macOS |

## v0.0.6 — Ejecutable unificado

Versión demo basada en un **único ejecutable `nexis`** que embebe el compilador y el intérprete: ya no hace falta descargar binarios separados (`nexisc`/`nexisi`).

### Artefactos

| Plataforma | Artefacto |
|---|---|
| **Linux (x86_64)** | [nexis-v0.0.6-x86_64](v0.0.6/nexis-v0.0.6-x86_64) — binario suelto. |
| **Windows (x86_64)** | [nexis-v0.0.6-x86_64.exe](v0.0.6/nexis-v0.0.6-x86_64.exe) — binario suelto. |

### Uso

```sh
nexis build <archivo.nxs>   # compila el programa
nexis run <archivo.nxs>     # compila y ejecuta
```

### Novedades de la versión

- Ordenamientos completos (burbuja, selección, inserción, quick, merge, counting) sobre `Vector<T>` y demás colecciones.
- Genéricos con plantillas (`template <type_full T>`), `foreach` en todas sus variantes, variables globales y scope.
- Structs y clases completas (`init`, `self`, métodos) y funciones avanzadas (parámetros por defecto, recursión mutua).
- Suite de **101 pruebas** verificación; detalles en la [guía de demostración](../../docs/demo-v0.0.6.md).

## v0.0.5 — Primer ejecutable unificado

Primera versión que reemplaza los binarios separados `nexisc`/`nexisi` por el ejecutable unificado `nexis` (mismos comandos: `nexis build` y `nexis run`).

### Artefactos

| Plataforma | Artefacto |
|---|---|
| **Linux (x86_64)** | [nexis-v0.0.5-x86_64](v0.0.5/nexis-v0.0.5-x86_64) — binario suelto. |
| **Windows (x86_64)** | [nexis-v0.0.5-x86_64.exe](v0.0.5/nexis-v0.0.5-x86_64.exe) — binario suelto. |

---

## v0.0.2 — Producto completo (actualización)

Segunda versión del lenguaje como producto instalable. Publicada el **2026-09-12**.

### Instaladores

| Plataforma | Artefacto |
|---|---|
| **Debian/Ubuntu (x86_64)** | [nexis-v0.0.2-linux-x86_64.deb](v0.0.2/nexis-v0.0.2-linux-x86_64.deb) — instala con `sudo dpkg -i`. |
| **Otras distros Linux (x86_64)** | [nexis-v0.0.2-linux-x86_64.tar.xz](v0.0.2/nexis-v0.0.2-linux-x86_64.tar.xz) — trae `install.sh` y `uninstall.sh`. |
| **Windows (x86_64)** | [nexis-v0.0.2-windows-x86_64.exe](v0.0.2/nexis-v0.0.2-windows-x86_64.exe) — instalador NSIS que instala en `%LOCALAPPDATA%\Nexis` y añade `bin\` al `PATH`. |
| **Debian/Ubuntu (aarch64)** | [nexis-v0.0.2-linux-aarch64.deb](v0.0.2/nexis-v0.0.2-linux-aarch64.deb) — instala con `sudo dpkg -i`. |
| **Otras distros Linux (aarch64)** | [nexis-v0.0.2-linux-aarch64.tar.xz](v0.0.2/nexis-v0.0.2-linux-aarch64.tar.xz) — trae `install.sh` y `uninstall.sh`. |
| **Windows (aarch64)** | [nexis-v0.0.2-windows-aarch64.exe](v0.0.2/nexis-v0.0.2-windows-aarch64.exe) — instalador NSIS que instala en `%LOCALAPPDATA%\Nexis` y añade `bin\` al `PATH`. |

### Contenido

- Compilador `nexisc` e intérprete `nexisi`, ambos en su versión `v0.0.2`.
- Documentación completa del lenguaje (`docs/`) actualizada: guía de instalación, librerías propias y catálogo de errores ampliado.
- Suite de tests del lenguaje (`tests/`).
- Extensión de VS Code (`nexis-0.0.2.vsix`).

### Cambios respecto a v0.0.1

- Compilador e intérprete regenerados con la versión actualizada del script de build.
- Documentación ampliada con `installation.md`, `librerias_propias.md` y catálogo de errores NX actualizado.
- Extensión actualizada a v0.0.2 (gramática realineada, `fs"…"`, `#inject`, 20 snippets e icono propio).

---

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
- Extensión de VS Code (`nexis-0.0.1.vsix`).

### Limitaciones de la demo v0.0.1

- El compilador y el intérprete implementan tipos, operadores, `Console` e interpolación `fs"…"`.
- No incluye aún control de flujo, funciones, POO, `try/catch` ni módulos reales (ver `COMPATIBILIDAD.md` dentro de los instaladores).

## Publicar una nueva versión

1. Crea `releases/nexis/<versión>/` y añade los instaladores como `nexis-<versión>-<plataforma>.<ext>`.
2. Añade un `README.md` describiendo qué incluye esa versión y qué soluciona respecto a la anterior.
3. Actualiza el [índice de releases](../README.md).