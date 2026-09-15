# Compiler v0.0.2 — Actualización

**Componente:** compiler · **Fecha:** 2026-09-12 · **Tipo:** Actualización

Segunda versión del compilador de Nexis (binario `nexisc`). Generado con `installer/scripts/build_component_releases.sh` (v0.0.2).

## Qué incluye esta versión

- Binario `nexisc` compilado desde el mismo workspace de Cargo que v0.0.1.
- `README.md` del compilador con documentación interna de la arquitectura (lexer, parser, semántica, codegen).
- `INSTALACION.md` (guía de instalación paso a paso).
- Paridad con el intérprete `nexisi` v0.0.2: mismos tipos, operadores, `Console`, interpolación `fs"…"` y códigos de error NX.

### Alcance

- Tipos: `int`, `float`, `double`, `char`, `string`, `bool`; inferencia con `auto` y constantes con `const`.
- Operadores: aritméticos (`+ - * / % **`), incremento/decremento, asignación compuesta (`+= -= *= /= %= **=`), comparación (`== != > < >= <=`) y lógicos (`&& || !`).
- Entrada/salida: `Console.print`, `Console.println` y `Console.input(text="...")`.
- Interpolación: `fs"...{variable}..."`.
- Comentarios: `#/`, `//`, `#/* */#`, `#{ }#`, `/* */` y `# ...`; `#inject` se acepta como directiva no-op.

## Artefactos

- [nexisc-v0.0.2-x86_64.zip](nexisc-v0.0.2-x86_64.zip)

## Cambios respecto a la anterior (v0.0.1)

- Binario regenerado con la versión actualizada del script de build.
- Paridad de versionado con el intérprete y el producto completo v0.0.2.

## Instalación desde el zip

Guía paso a paso para Linux, Windows (PowerShell) y macOS:

- [Descargar e instalar `nexisc`](../../../docs/installation.md) — también incluida como `INSTALACION.md` dentro de cada `.zip`.

## Uso

```sh
nexisc <archivo.nxs>
nexisc --help
nexisc --version   # nexisc 0.0.2 (Nexis)
```
