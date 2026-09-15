# Interpreter v0.0.2 — Actualización

**Componente:** interpreter · **Fecha:** 2026-09-12 · **Tipo:** Actualización

Segunda versión del intérprete de Nexis (binario `nexisi`). Generado con `installer/scripts/build_component_releases.sh` (v0.0.2).

## Qué incluye esta versión

- Binario único `nexisi` (sin dependencias de runtime).
- `README.md` del intérprete.
- `INSTALACION.md` (guía de instalación paso a paso).
- Paridad con el compilador `nexisc` v0.0.2: mismos tipos, operadores, `Console`, interpolación `fs"…"` y códigos de error NX.

## Qué hace

- `nexisi programa.nxs` — ejecuta un archivo (backend tree-walk, paridad 1:1 con `nexisc`).
- `nexisi --bytecode programa.nxs` — ejecuta con el backend bytecode de la VM.
- `nexisi --debug programa.nxs` — ejecuta con trazas.
- `nexisi --repl` — consola interactiva persistente.

## Artefactos

| Plataforma | Artefacto |
|---|---|
| Linux (x86_64) | [nexisi-v0.0.2-linux-x86_64.zip](nexisi-v0.0.2-linux-x86_64.zip) |

## Cambios respecto a la anterior (v0.0.1)

- Binario regenerado con la versión actualizada del script de build.
- Paridad de versionado con el compilador y el producto completo v0.0.2.

## Instalación (Linux)

```bash
unzip nexisi-v0.0.2-linux-x86_64.zip -d nexisi
cd nexisi
mkdir -p ~/.local/bin
install -m 755 nexisi ~/.local/bin/
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
nexisi --version
```

## Verificación

Paridad garantizada por `interpreter/scripts/run_interpreter_tests.sh` (mismas salidas y errores que `nexisc`).
