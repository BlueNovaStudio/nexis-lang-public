# v0.0.1 — Interpreter (Release inicial)

## Artefacto

| Plataforma | Artefacto |
|---|---|
| Linux (x86_64) | [nexisi-v0.0.1-linux-x86_64.zip](nexisi-v0.0.1-linux-x86_64.zip) |

Se genera con `interpreter/scripts/release.sh` (estructura análoga a la del compilador).

## Qué incluye

- Binario único `nexisi` (sin dependencias de runtime).
- `README.md` del intérprete.
- `INSTALACION.md` (manual de instalación).

## Qué hace

- `nexisi programa.nxs` — ejecuta un archivo (backend tree-walk, paridad 1:1 con `nexisc`).
- `nexisi --bytecode programa.nxs` — ejecuta con el backend bytecode de la VM.
- `nexisi --debug programa.nxs` — ejecuta con trazas.
- `nexisi --repl` — consola interactiva persistente.

## Instalación (Linux)

```bash
unzip nexisi-v0.0.1-linux-x86_64.zip -d nexisi
cd nexisi
mkdir -p ~/.local/bin
install -m 755 nexisi ~/.local/bin/
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
nexisi --version
```

## Verificación

Paridad garantizada por `interpreter/scripts/run_interpreter_tests.sh` (mismas salidas y errores que `nexisc`).