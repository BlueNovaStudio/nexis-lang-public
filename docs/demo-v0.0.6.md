# 🎬 Guía de demostración — Nexis V0.0.6

Esta guía reúne todo lo necesario para **compilar, ejecutar y demostrar**
las capacidades de Nexis V0.0.6: ordenamientos, genéricos, `foreach`
avanzado, globales, structs/clases, colecciones y funciones.

---

## 1. Requisitos

- Rust y Cargo instalados (`rustc --version`, `cargo --version`).
- PowerShell (Windows) o una shell POSIX (Linux/macOS).
- El repositorio clonado en `nexis-lang/`.

---

## 2. Compilar

```powershell
cargo build --manifest-path compiler/Cargo.toml
```

El binario de desarrollo queda en:

```
compiler\target\debug\nexisc.exe
```

Para una compilación optimizada:

```powershell
cargo build --release --manifest-path compiler/Cargo.toml
```

El binario de release queda en:

```
compiler\target\release\nexisc.exe
```

Comprobar la versión:

```powershell
compiler\target\release\nexisc.exe --version
# nexis 0.0.6
```

---

## 3. Ejecutar un programa

```powershell
compiler\target\debug\nexisc.exe ruta\al\programa.nxs
```

Si el programa usa `Console.input(...)`, escribe cada respuesta en una
línea nueva.

---

## 4. Demos principales

| Archivo | Qué demuestra |
|---------|----------------|
| `compiler/examples/00_variables.nxs` | Tipos, constantes, operadores, precedencia. |
| `compiler/examples/01_condicionales.nxs` | `if`/`else if`/`else`, `switch`, lógicos. |
| `compiler/examples/02_bucles.nxs` | `while`, `do while`, `for`, `foreach`, `break`/`continue`. |
| `compiler/examples/03_funciones.nxs` | Funciones con y sin retorno, recursión. |
| `compiler/examples/04_errores.nxs` | `try`/`catch`/`finally`, errores personalizados. |
| `compiler/examples/05_estructuras.nxs` | Vector, LinkedList, Stack, Queue, Map, Set, Tree, Trie, Graph. |
| `compiler/examples/06_librerias.nxs` | `math`, `string`, `random`, `time`, `file`. |
| `compiler/examples/08_integrador.nxs` | Agenda de contactos: structs, menú, búsqueda, listado. |

### Entradas sugeridas para la demo

| Demo | Entrada (una por línea) |
|------|--------------------------|
| `01_condicionales` | `5`, `3`, `4`, `5`, `7`, `a` |
| `05_estructuras` | `(a+b)` |
| `06_librerias` | `16`, `2`, `Hola Mundo` |
| `08_integrador` | `1`, `Ana`, `123`, `1`, `Luis`, `456`, `3`, `2`, `Luis`, `0` |

Ejemplo en PowerShell:

```powershell
"5`n3`n4`n5`n7`na" | compiler\target\debug\nexisc.exe compiler\examples\01_condicionales.nxs
```

---

## 5. Demos avanzados (V0.0.6)

Los archivos de `tests/10_avanzado/` son la demostración técnica de las
novedades. Todos tienen salida esperada en `tests/expected/`.

### 5.1 Todos los ordenamientos

`tests/10_avanzado/01_ordenamientos_vector.nxs`

- Burbuja, selección, inserción, quick sort, merge sort y counting sort.
- Todos sobre `Vector<int>` y con acceso `v[j + 1]`.

```
burbuja: [5, 11, 12, 22, 25, 34, 64, 90]
seleccion: [5, 11, 12, 22, 25, 34, 64, 90]
insercion: [5, 11, 12, 22, 25, 34, 64, 90]
quick: [5, 11, 12, 22, 25, 34, 64, 90]
merge: [5, 11, 12, 22, 25, 34, 64, 90]
counting: [5, 11, 12, 22, 25, 34, 64, 90]
```

### 5.2 Ordenar en todas las estructuras

`tests/10_avanzado/02_ordenamientos_estructuras.nxs`

- Burbuja manual sobre `LinkedList` con `lista[j + 1]`.
- `sort()` y `reverse()` en `LinkedList`, `Stack` y `Queue`.
- Orden lexicográfico de `Vector<string>`.
- Ordenar structs por un campo.

### 5.3 Genéricos

`tests/10_avanzado/03_genericos_plantillas.nxs`

```
template <type_full T>
func contiene(Vector<T>: lista, T: objetivo) -> bool { ... }
```

La misma función sirve para `Vector<int>`, `Vector<string>` y
`Vector<double>`.

### 5.4 `foreach` en todas sus formas

`tests/10_avanzado/04_foreach_variantes.nxs`

- `foreach (p in productos)`
- `foreach (p, productos)`
- `foreach (string p, productos)`
- `foreach (char c, frase)`
- `break` y `continue`
- `foreach` anidado
- `foreach` sobre `LinkedList`

### 5.5 Globales y scope

`tests/10_avanzado/05_globales_y_scope.nxs`

- Una función lee y modifica un contador global.
- Una función añade a un vector global.
- Shadowing: la local no cambia la global.

### 5.6 Structs y clases

`tests/10_avanzado/06_structs_clases.nxs`

- Structs dentro de `Vector`.
- Búsqueda con `foreach (Contacto c, agenda)`.
- Clase con `init`, `self` y métodos que modifican estado.
- Ordenar structs por nombre.

### 5.7 Funciones avanzadas

`tests/10_avanzado/07_funciones_avanzadas.nxs`

- Parámetros por defecto.
- Recursión simple y mutua.
- Funciones que devuelven `Vector<int>`.
- Composición de funciones.

### 5.8 Matrices y búsqueda

`tests/10_avanzado/08_matrices_y_busqueda.nxs`

- `Vector<Vector<int>>`.
- Búsqueda lineal y binaria.
- Suma de filas y transpuesta.

---

## 6. Ejecutar la suite completa

```powershell
powershell -ExecutionPolicy Bypass -File tests/run_tests.ps1
```

Resultado esperado en V0.0.6:

```
Resultado: 101 correctos, 0 fallidos, 101 total
```

Filtrar por carpeta:

```powershell
powershell -ExecutionPolicy Bypass -File tests/run_tests.ps1 -Filter "*10_avanzado*"
```

La suite:

- ejecuta cada `.nxs` de `compiler/examples` y `tests`;
- toma la entrada de `tests/inputs/<ruta>.txt` si existe;
- compara la salida con `tests/expected/<ruta>.txt` si existe;
- exige el código `NXxx` en los archivos `*_error_nxNN_*`;
- exige `NX81` en los casos de importación circular.

---

## 7. Guion sugerido para la demo

1. **Variables y control** (`00` y `01`): mostrar tipos, operadores y
   `switch`.
2. **Bucles** (`02`): `for i in 0 ... n`, `foreach` y `break`/`continue`.
3. **Funciones** (`03` y `07`): recursión, parámetros por defecto y
   funciones que devuelven colecciones.
4. **Genéricos** (`03_genericos_plantillas`): la misma función con
   `int`, `string` y `double`.
5. **Ordenamientos** (`01_ordenamientos_vector` y
   `02_ordenamientos_estructuras`): bubble, selection, insertion, quick,
   merge, counting; luego `sort()` en cada colección.
6. **Colecciones** (`05_estructuras`): Vector, Stack, Queue, Map, Set,
   Tree, Trie y Graph.
7. **POO** (`06_structs_clases`): structs, clases, `init`, `self`.
8. **Globales** (`05_globales_y_scope`): funciones que modifican estado
   compartido.
9. **Integrador** (`08_integrador`): agenda de contactos completa.

---

## 8. Estructura del proyecto

| Carpeta | Contenido |
|---------|-----------|
| `compiler/crates/nexis_lexer` | Análisis léxico. |
| `compiler/crates/nexis_parser` | Análisis sintáctico y AST. |
| `compiler/crates/nexis_sema` | Análisis semántico y tipos. |
| `compiler/crates/nexis_codegen` | Intérprete del AST. |
| `compiler/examples` | Programas de demostración. |
| `tests/` | Suite de pruebas y casos de error. |
| `docs/` | Documentación del lenguaje y de la librería estándar. |

Los archivos de código se mantienen por debajo de ~800 líneas; cuando un
módulo crece se separa en archivos hermanos (`helpers.rs`, `coerce.rs`,
etc.) para que los cambios no rompan todo el proyecto.

---

## 9. Problemas frecuentes

| Síntoma | Causa / solución |
|---------|------------------|
| `No se encontró nexisc.exe` | Compila primero con `cargo build`. |
| `NX11` al ordenar | Usar `0 ... n` (exclusivo) o `0 .. (n - 1)`. |
| `NX50` al desapilar | Comprobar `isEmpty()` antes de `pop`/`dequeue`. |
| `NX52` en un `Map` | Comprobar `contains(clave)` antes de `get`. |
| `NX60` al leer entrada | El texto no es convertible al tipo pedido. |
| La salida se pega sin saltos | Usar `Console.println` en lugar de `Console.print`. |
| `NX81` al importar | Hay una importación circular entre módulos. |

---

## 10. Cierre

V0.0.6 cubre el ciclo completo: variables, control de flujo, funciones,
genéricos, colecciones, POO, errores y una suite de 101 pruebas. La
documentación de cada tema está enlazada desde
[`docs/README.md`](README.md).
