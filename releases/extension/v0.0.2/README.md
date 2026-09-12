# Extension v0.0.2 — Actualización completa

**Componente:** extension · **Fecha:** 2026-09-10 · **Tipo:** Actualización

Replanteamiento completo de la gramática TextMate para que **diga lo que Nexis es** (no lo que parecía), alineada con la documentación del lenguaje y con `compiler/tokens-en-accion/`.

## Qué incluye esta versión

- **Gramática realineada**: keywords, tipos y operadores reales del lenguaje (se eliminan las decenas de palabras inventadas de v0.0.1).
- `#builtins` corregido e incluido: `Console.print/println/input`, `math.*`, `string.*`, `file.*`, `time.*`, `random.*`, `graphics.*`, `network.*` sí se resaltan ahora.
- Cadena interpolada `fs"…"`, caracteres `'c'` y secuencias de escape.
- Directiva `#inject modulo;` / `#inject "ruta.nex";`.
- Declaración y llamadas de funciones genéricas (se elimina el hack `ProcesarPago`/`RechazarTransaccion`).
- Generics `Vector<int>` sin colorear `< >` como comparación.
- Snippets (20 atajos: `inject`, `func`, `if`, `for`, `Console.print`, `tryc`, `class`…).
- Icono propio (`images/logo.png`) y branding NEXIS.
- Manual interno [`docs/extension/README.md`](docs/extension/README.md): arquitectura, orden de patrones, scopes y cómo ampliar la extensión.
- `language-configuration.json` con las 3 formas de comentario de bloque de Nexis (`/* */`, `#/* */#`, `#{ }#`).
- `package.json` reescrito: nombre `nexis`, display `NEXIS`, icono y snippets declarados.

## Cambios respecto a la anterior (v0.0.1)

- v0.0.1 solo resaltaba `//` y `/* */` (no reconocía `#/* */#`, `#{ }#`, `#/` ni el `#` genérico).
- v0.0.1 no resaltaba `Console.print` ni la biblioteca estándar (repositorio `builtings` estaba definido pero nunca incluido).
- v0.0.1 tenía decenas de keywords y tipos inventados (`elif`, `using`, `import`, `async`, `int8`…`uint64`, `decimal`, `var`…), sin `#inject`, sin `fs"…"`, sin `'c'`, sin snippets, sin generics.
- v0.0.1 no tenía icono ni identidad NEXIS.

## Artefactos

- [nexis-0.0.2.vsix](nexis-0.0.2.vsix)

> El código fuente de la extensión se mantiene en el repositorio privado de desarrollo de Nexis (nexis-lang).
