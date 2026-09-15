# 🔧 Cómo funciona esta extensión

Esta guía explica **por dentro** cómo funciona la extensión de Visual Studio Code para el lenguaje **Nexis**. Está pensada para quien quiera mantener, depurar o ampliar la extensión y necesita entender el papel de cada archivo, cómo tokeniza el resaltado de sintaxis y por qué el orden de los patrones es tan importante.

---

## 1. Índice

- [1. Índice](#1-índice)
- [2. Estructura de la extensión](#2-estructura-de-la-extensión)
- [3. Manifiesto `package.json`](#3-manifiesto-packagejson)
- [4. La gramática TextMate](#4-la-gramática-textmate)
  - [4.1 Qué es una gramática TextMate](#41-qué-es-una-gramática-textmate)
  - [4.2 El orden importa](#42-el-orden-importa)
  - [4.3 Repositorios (catálogo de patrones)](#43-repositorios-catálogo-de-patrones)
  - [4.4 Scopes usados](#44-scopes-usados)
- [5. Configuración de lenguaje `language-configuration.json`](#5-configuración-de-lenguaje-language-configurationjson)
- [6. Snippets](#6-snippets)
- [7. Cómo se cargan las piezas en VS Code](#7-cómo-se-cargan-las-piezas-en-vs-code)
- [8. Probar y depurar](#8-probar-y-depurar)
- [9. Empacar y publicar](#9-empacar-y-publicar)
- [10. Ampliar la extensión paso a paso](#10-ampliar-la-extensión-paso-a-paso)
- [11. Limitaciones actuales y vías de mejora](#11-limitaciones-actuales-y-vías-de-mejora)

---

## 2. Estructura de la extensión

```
extension/
├── package.json                 → Manifiesto de VS Code (declara lo que la extensión aporta)
├── language-configuration.json  → Comentarios, brackets y auto-cierre
├── syntaxes/
│   └── nexis.tmLanguage.json    → La gramática TextMate (resaltado de sintaxis)
├── snippets/
│   └── nexis.code-snippets      → Snippets (func, if, for, Console.*, etc.)
├── images/
│   └── logo.png                 → Icono de la extensión y del lenguaje
├── .vscode/
│   └── launch.json              → Configuración F5 para probar la extensión (Extension Host)
├── docs/                        → Documentación del LENGUAJE (copia de /docs)
│   ├── extension/               → Este manual de la extensión
│   └── README.md                → Índice de la documentación del lenguaje
├── versions/                    → Paquetes .vsix publicados (histórico)
├── CHANGELOG.md                 → Registro de versiones (por qué cambia cada cosa)
└── README.md                    → Portada: qué es, instalación, versión actual y su balance
```

> ⚠️ **Importante:** `package.json`, `language-configuration.json` y `*.tmLanguage.json` son **JSON puro**: no admiten comentarios `//`. Por eso toda la documentación *dentro* de la gramática vive en la clave `"comment"` de cada patrón (que TextMate sí entiende), y el resto se explica en este documento.

---

## 3. Manifiesto `package.json`

El manifiesto le dice a VS Code **qué** aporta la extensión y **cuándo** activarse.

| Campo | Qué hace |
|-------|----------|
| `name`, `displayName`, `publisher`, `version` | Identidad y versión. `version` es la que define el `.vsix`. |
| `engines.vscode` | Versión mínima de VS Code compatible (`^1.60.0`). |
| `contributes.languages` | Registra el lenguaje: `id: "nexis"`, alias `Nexis`, extensión de archivo `.nxs`, icono y su `configuration` (la config de lenguaje). |
| `contributes.grammars` | Asocia el lenguaje `nexis` con la gramática TextMate: `scopeName: "source.nexis"` y la ruta al `.tmLanguage.json`. **La coincidencia lanzador-gramática es por `scopeName`**, no por el nombre. |
| `contributes.snippets` | Asocia los snippets al lenguaje `nexis`. Sin esto, los snippets no se ofrecerían en `.nxs`. |

**Cómo se dispara la tokenización:** cuando abres un `.nxs`, VS Code resuelve el language ID `nexis` desde `contributes.languages.extensions`, busca el grammar cuyo `language` coincida y empieza a colorear con el `scopeName` `source.nexis`.

---

## 4. La gramática TextMate

### 4.1 Qué es una gramática TextMate

`nexis.tmLanguage.json` es una gramática TextMate en formato JSON. Funciona como un conjunto de **expresiones regulares Oniguruma** organizadas para "pintar" tramos de texto con scopes. Un scope es una etiqueta jerárquica como `keyword.control.nexis` o `string.quoted.double.nexis`; el *tema* de color de VS Code decide qué color darle a cada scope.

Reglas básicas:

- Un **patrón** es un objeto con una clave `match` (una línea) o `begin`/`end` (multilínea, por ejemplo comentarios de bloque o cadenas).
- Los patrones se agrupan en **repositorios** (`"repository"`) como `#keywords`, `#strings`, etc.
- El array superior `"patterns"` decide el **orden global** en que se prueban los repositorios.
- TextMate recorre el texto de izquierda a derecha y, en cada posición, **prueba los patrones en orden hasta que uno encaja**. El primero que encaje *consume* ese tramo. Por eso el orden es decisivo.

### 4.2 El orden importa

El orden top-level de esta gramática es:

```
1. #directives     2. #functions     3. #builtins     4. #keywords
5. #generics       6. #types         7. #function-calls  8. #class-names
9. #strings       10. #comments     11. #numbers      12. #operators
```

¿Por qué exactamente este orden?

| Regla | Motivo |
|-------|--------|
| `#directives` primero | `#inject` empieza con `#`. Si comentarios o números fueran antes, el `#` se comería la directiva como comentario. |
| `#functions` antes de `#keywords` | Para que `func suma(` y `void main(` capturen `func`/`void` como keyword **y** el nombre como función, todo en un solo patrón. |
| `#builtins` antes de keywords/tipos | `Console.print`, `math.pow`, `string.longitud`… deben ganar a `Console` (PascalCase) y a `string` (tipo). |
| `#keywords` antes de `#function-calls` | `if(`, `while(`, `switch(` no deben colorearse como llamadas. |
| `#generics` antes de `#types` | `Vector<int>` debe consumirse entero; si `#types` pasara antes, el patrón de colección robaría `Vector` y `<`/`>` se pintarían como comparación. |
| `#types` antes de `#function-calls` | `string` (tipo) no debe convertirse en llamada aunque luego venga un `(`. |
| `#function-calls` antes de `#class-names` | `ProcesarPago()` es una función; `Cuenta miCuenta` es una clase. Colorear llamadas primero da mejor resultado en identificadores PascalCase. |
| `#strings` y `#comments` antes de `#numbers`/`#operators` | el contenido de un string o comentario no debe reinterpretarse como números u operadores. |
| `#numbers` antes de `#operators` | `3.14` debe salir entero como float; si el operador `.` fuera antes, se trocearía. |

### 4.3 Repositorios (catálogo de patrones)

Todos los repositorios están documentados con su clave `"comment"` *in situ*. Resumen:

| Repositorio | Qué colorea | Patrones claves |
|-------------|-------------|-----------------|
| `#directives` | `#inject nombre;` y `#inject "ruta.nex";` | begin `#inject`, end `;`; dentro: librería (módulo) o cadena |
| `#functions` | `func nombre(...)` y `void nombre(...)` | capture 1 → `keyword.control.function`, capture 2 → `entity.name.function` |
| `#builtins` | `Console.print/println/input`, módulos `math`, `string`, `file`, `time`, `random`, `graphics`, `network` y globales `imprimir_error`, `terminar`, `afirmar` | un patrón por módulo con captures módulo→`support.class`, función→`support.function` |
| `#keywords` | Reservadas de control (`if`, `for`, `in`, `step`, `break`…), de errores (`try`, `catch`, `finally`, `throw`, `lanzar`) y otras (`func`, `emit`, `class`, `struct`) | coinciden con `\b…\b` |
| `#generics` | `Vector<T>`, `Map<K,V>`, etc. | begin `Coleccion<`, end `>`; interior reutiliza `#types` |
| `#types` | `int float double char string bool void auto const`, `true/false`, errores nativos `Error*` y colecciones sin `<` | patrones de tipo, booleano, clase-error, clase-colección |
| `#function-calls` | Cualquier `identificador(` no reservado (funciones/métodos del usuario) | `\b\w+(?=\s*\()` |
| `#class-names` | Identificadores en PascalCase (`Cuenta`, `ErrorSaldoInsuficiente`) | `\b[A-Z][a-z][\w]*\b` (exige segunda minúscula para no pintar constantes en MAYÚSCULAS) |
| `#strings` | `fs"…"` (interpolado, `{expr}` coloreado), `"…"` (escapes), `'c'` (carácter) | begin/end con patrones internos de escape e interpolación |
| `#comments` | `#/* */#`, `#{ }#`, `/* */` (bloques), `#/`, `//` (línea) y `#…` (genérico) | bloques **antes** que líneas para no romper aperturas |
| `#numbers` | `0xFF`, `0b1010`, `3.14`, `3.14f`, `2.5e3`, `077`, `42` | hex, binario, float (con `f`/exponente), octal, entero |
| `#operators` | `=> <-->`, `->`, `... ..`, `:=`, comparación, asignación, aritmética, lógica, `.` | alternancias de mayor a menor longitud |

**Regla de oro del orden interno:** en cada repositorio, los patrones *más específicos/largos* van primero (compuestos antes que simples):
- `**=` antes que `*=` y `=`
- `==` antes que `=`
- `=>` antes que `>` y `=`
- `++`, `--`, `**` antes que `+`, `-`, `*`
- `..` y `...` antes que `.`
- comentarios de bloque antes que comentarios de línea
- floats antes que enteros

### 4.4 Scopes usados

La gramática produce estos scopes (los temas pueden colorearlos todos o ignorar los que no conozcan):

```
source.nexis
├── meta.directive.inject.nexis        keyword.directive.inject.nexis / entity.name.module.nexis
├── meta.function.declaration.nexis    keyword.control.function.nexis / entity.name.function.nexis
├── meta.type.generic.nexis            support.class.collection.nexis / punctuation.definition.typeparameters.*
├── keyword.control.nexis              (if, else, for, while, do, foreach, switch, case, default,
│                                       break, continue, in, step)
├── keyword.control.exception.nexis    (try, catch, finally, throw, lanzar)
├── keyword.other.nexis                (func, emit, class, struct)
├── keyword.directive.inject.nexis
├── storage.type.nexis                 (int, float, double, char, string, bool, void, auto, const)
├── constant.language.boolean.nexis    (true, false)
├── support.class.exception.nexis      (Error, ErrorIndice, ErrorDivision, ErrorMatematico, ErrorTipo,
│                                       ErrorValidacion, ErrorMemoria, ErrorArchivo, ErrorEntrada,
│                                       ErrorRed, ErrorGrafico, ErrorAssert)
├── support.class.collection.nexis     (Vector, Stack, Queue, Set, Map, LinkedList, Tree, Graph, Trie)
├── support.class.nexis                (Console y módulos: math, string, file, time, random, graphics, network)
├── support.function.console.nexis     (print, println, input)
├── support.function.<modulo>.nexis    (funciones de cada módulo)
├── support.function.global.nexis      (imprimir_error, terminar, afirmar)
├── entity.name.function.nexis         (declaraciones y llamadas)
├── entity.name.class.nexis            (clases en PascalCase)
├── string.interpolated.nexis          constant.other.interpolation.nexis / constant.character.escape.nexis
├── string.quoted.double.nexis         constant.character.escape.nexis
├── string.quoted.single.nexis
├── comment.block.hash.nexis / comment.block.nexis
├── comment.line.hash-slash.nexis / comment.line.double-slash.nexis / comment.line.number-sign.nexis
├── constant.numeric.{hex,binary,float,octal,integer}.nexis
└── keyword.operator.{ternary,arrow,range,inference,comparison,assignment,arithmetic,logical,member}.nexis
```

---

## 5. Configuración de lenguaje `language-configuration.json`

Este archivo **no colorea**: configura comportamientos de edición del lenguaje.

| Clave | Qué hace |
|-------|----------|
| `comments.lineComment` | `"//"` — lo que inserta **Ctrl+/** (toggle). Solo admite uno; se eligió `//` por ser universal (tanto `#/` como `//` son comentarios válidos en Nexis). |
| `comments.blockComment` | Array de pares `{open, close}` con las **tres** formas de comentario de bloque: `/* */`, `#/* */#` y `#{ }#`. VS Code usa estos pares para el toggle de bloque y el auto-cierre. |
| `brackets` | Pares `{}`, `[]`, `()` para indentación automática y coincidencia de llaves. |
| `autoClosingPairs` | Auto-cierre al teclear: `{}`, `[]`, `()`, `"……"`, `'…'`. |
| `surroundingPairs` | Lo que se puede usar con la acción "rodear selección". |

---

## 6. Snippets

`snippets/nexis.code-snippets` define los snippets que aparecen al teclear el prefijo en un `.nxs`. Se declaran en `package.json` con `contributes.snippets.language: "nexis"`.

Snippets disponibles (prefijo → qué genera):

| Prefijo | Genera |
|---------|--------|
| `inject` | `#inject modulo;` |
| `injectf` | `#inject "ruta/archivo.nex";` |
| `func` | función `func nombre(params) -> tipo { }` |
| `voidfn` | función `void nombre(params) { }` |
| `if`, `ife` | `if (cond) { }` / `if/else` |
| `for`, `forstep` | `for i in a .. b { }` / con `step N` |
| `foreach` | `foreach (item in colección) { }` |
| `while` | `while (cond) { }` |
| `switch` | `switch (expr) { case …: }` |
| `tryc`, `trycf` | `try/catch` y `try/catch/finally` |
| `p`, `pl`, `input` | `Console.print`, `Console.println`, `Console.input` |
| `class`, `struct` | esqueleto de clase / struct |
| `emit` | `emit -> valor` |
| `tern` | operador `(cond) => a <--> b` |

Los snippets usan `$1`, `$2`, `…` y `${1:default}` como posiciones de tabulación; `$0` es la posición final del cursor.

---

## 7. Cómo se cargan las piezas en VS Code

Al arrancar VS Code con la extensión activa, el orden de carga es:

1. VS Code lee `package.json` → conoce el language `nexis`, la gramática, la configuración y los snippets.
2. Cuando abres un `.nxs`, asigna el language `nexis` y lee `language-configuration.json` (comportamiento de edición).
3. El engine TextMate carga `nexis.tmLanguage.json` y tokeniza cada línea. La tokenización genera scopes.
4. El tema de color activo mapea los scopes a colores (los scopes desconocidos quedan con el color por defecto).
5. El `Chat`/`Quick Fix` nada más: esta extensión es **solo sintaxis** (no hay IntelliSense, hover ni validación semántica todavía).

---

## 8. Probar y depurar

**Lanzar en modo desarrollo (Extension Host):**
1. Abre la carpeta `extension/` en VS Code.
2. Pulsa `F5` (usa `.vscode/launch.json`). Se abre otra ventana de VS Code con la extensión cargada.
3. Crea un archivo `.nxs` y comprueba el coloreado.
4. Tras tocar la gramática, recarga con `Ctrl+R` (o `Cmd+R`).

**Inspeccionar los scopes:**
- Abre la Paleta de comandos (`Ctrl+Shift+P`) → *Developer: Inspect Editor Tokens and Scopes*.
- Coloca el cursor sobre un token; verás el scope asignado (p. ej. `keyword.control.nexis`). Así puedes comprobar si un patrón está ganando cuando debería.

**Automatizado (recomendado para regresiones):**
La gramática se puede probar fuera de VS Code con `node`:

```bash
npm i -D vscode-textmate vscode-oniguruma   # en un proyecto de pruebas
```

y un script que tokenice un `.nxs` y muestre `texto·scope` por token. Esto permite verificar que `#inject`, las cadenas `fs"…"`, los ternarios `=> <-->` y los comentarios de bloque se respetan tras cada cambio. (El script de esta sesión se usó para validar todos los ejemplos de `compiler/examples/`.)

---

## 9. Empacar y publicar

Requiere la CLI de Microsoft:

```bash
npm i -g @vscode/vsce
vsce package          # genera nexis-0.0.X.vsix
vsce publish          # publica en el Marketplace (requiere cuenta de editor)
```

El `.vsix` generado se puede instalar manualmente desde el menú *Extensions* → `…` → *Install from VSIX…*. El histórico de `.vsix` se guarda en `versions/` como registro.

> Antes de publicar, revisa `README.md`, `CHANGELOG.md`, el icono y la licencia (`LICENSE.txt`).

---

## 10. Ampliar la extensión paso a paso

**Añadir un snippet:**
1. Edita `snippets/nexis.code-snippets` (JSON) con un bloque `{ "nombre": { "prefix", "body", "description" } }`.
2. Recarga la ventana (`Ctrl+R`).

**Colorear una nueva palabra reservada:**
1. Abre `syntaxes/nexis.tmLanguage.json`.
2. Añade la palabra a la lista del repositorio apropiado (`#keywords`, `#types`…), respetando que las palabras más largas vayan primero en las alternancias.
3. Si es una palabra que puede confundirse con otra regla (como un `#`), comprueba que el repositorio se incluya en la posición correcta del array `patterns`.

**Colorear una función nueva de un módulo:**
Añade el nombre a la lista del patrón de ese módulo en `#builtins`. Mantén las alternancias ordenadas (de más largas a más cortas no es crítico aquí porque son nombres completos, pero es buena práctica).

**Añadir un operador:**
Agrega el símbolo al patrón adecuado en `#operators`. **Siempre** colócalo *antes* que el símbolo más corto que lo contenga (`**=` antes que `=`; `=>` antes que `>`). Y verifica con el script de test que no rompe combinaciones existentes.

**Añadir un comentario de bloque nuevo:**
Añádelo en `#comments` **antes** de los comentarios de línea, y añade el par a `comments.blockComment` en `language-configuration.json`.

---

## 11. Limitaciones actuales y vías de mejora

Esta es una extensión **solo de sintaxis**. Cosas que NO hace y que podrían añadirse en el futuro:

| Limitación | Posible mejora |
|------------|----------------|
| Sin IntelliSense (autocompletado de métodos de `Console`, módulos, nombres de clase) | Implementar un servidor de lenguaje (LSP) o un `vscode-languageserver` ligero |
| Sin *hover* ni *go-to-definition* | LSP con índices de símbolos |
| Sin validación/diagnóstico de errores NX | LSP que reutilice los códigos NX de la documentación (`NX02`, `NX43`…) |
| Sin `did-change` de plantillas ni formateador | No existe formateador oficial del lenguaje aún |
| La gramática no distingue el `:` de parámetro/`if`/mapa (se deja sin scope) | Añadir patrones `punctuation` específicos si molesta visualmente |
| El snippet de `switch` asume estructura clásica | Versiones alternativas para rangos (`case 90 ... 100:`) |
| `lineComment` único (`//`): no hay toggle nativo para `#/` | Aceptar `#/` manualmente o valorar cambiar el `lineComment` en una futura versión |

Cualquier cambio debe registrarse en `CHANGELOG.md` — el repositorio usa el *registro de versiones* para documentar lo bueno y lo malo de cada versión y el porqué de cada decisión.