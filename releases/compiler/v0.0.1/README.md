# Compiler v0.0.1 — Release inicial

**Componente:** compiler · **Fecha:** 2026-09-09 · **Tipo:** Release inicial

Primera versión funcional del compilador de Nexis (binario `nexisc`). En esta versión el binario **interpreta y ejecuta directamente** los programas `.nxs` en lugar de generar código objeto.

## Qué incluye esta versión

Workspace de Cargo en `compiler/` con las fases del compilador como crates:

| Paquete | Rol |
|---|---|
| `nexisc` | Binario CLI: orquesta las fases y reporta errores NX |
| `nexis_ast` | AST: tipos, valores, expresiones y sentencias |
| `nexis_lexer` | Tokenización: literales, operadores, comentarios y `fs"..."` |
| `nexis_parser` | Síntaxis con precedencia de operadores y uso de `auto`/`const` |
| `nexis_sema` | Validación semántica (códigos NX00–NX10, NX60, NX91) |
| `nexis_codegen` | Ejecución: intérprete con entrada/salida de consola |
| `nexis_errors` | Catálogo de errores y reporte con ubicación línea/columna |

### Alcance de la versión (variables)

- Tipos: `int`, `float`, `double`, `char`, `string`, `bool`; inferencia con `auto` y constantes con `const`.
- Operadores: aritméticos (`+ - * / % **`), incremento/decremento, asignación compuesta (`+= -= *= /= %= **=`), comparación (`== != > < >= <=`) y lógicos (`&& || !`).
- Entrada/salida: `Console.print`, `Console.println` (con salto de línea) y `Console.input(text="...")`.
- Interpolación: `fs"...{variable}..."`.
- Comentarios: `#/`, `//`, `#/* */#`, `#{ }#`, `/* */` y `# ...`; `#inject` se acepta como directiva no-op.

## Uso

```sh
cargo build --release
./target/release/nexisc <archivo.nxs>
```

Con ayuda y versión:

```sh
nexisc --help
nexisc --version   # nexisc 0.0.1 (Nexis)
```

## Instalación desde el zip

Guía paso a paso para Linux, Windows (PowerShell) y macOS:

- [Descargar e instalar `nexisc`](../../../docs/installation.md) — también incluida como `INSTALACION.md` dentro de cada `.zip`.

## Generar los instaladores (Linux, Windows y macOS)

Un solo comando compila para las tres plataformas y deja los `.zip` aquí:

```sh
compiler/scripts/release.sh --all
```

- `nexisc-v<versión>-linux-x86_64.zip`
- `nexisc-v<versión>-windows-x86_64.zip` (el `.exe`)
- `nexisc-v<versión>-mac-x86_64.zip`

Desde Linux, macOS y Windows se compilan con **Docker + cross** (requisitos: `sudo apt install docker.io` y activar el daemon). Windows también se puede compilar sin Docker instalando `gcc-mingw-w64-x86-64`.

El script detecta la versión de `compiler/Cargo.toml`; se omite con `--version <v>`. Otros flags: `--linux`, `--windows`, `--mac`, `--skip-zip`, `--help`.

## Cambios respecto a la anterior

- Primera release del componente; no existe versión anterior.