# Catálogo de errores: Entrada/salida, módulos, red y sistema (NX60–NX99)

Parte del [catálogo de errores de Nexis](errors.md). Cada código
incluye descripción, causa, ejemplo, solución paso a paso y cómo
evitarlo.

# Categoría: Entrada/Salida y archivos (NX60–NX69)

## NX60: Formato de entrada inválido

**Descripción.** En `Console.input`, el usuario ingresó un **valor que no se puede convertir al tipo esperado**: por ejemplo, escribir `"veinte"` cuando la variable es `int`. Se corresponde con `ErrorEntrada` o `ErrorValidacion`.

**Causa común.** No validar la entrada y asumir que el usuario siempre teclea lo correcto.

**Ejemplo que lo genera.**

```
int edad = Console.input(text="Ingrese su edad: ")
// el usuario ingresa "veinte" → NX60
```

**Solución paso a paso.**

1. Pide la entrada como `string` y valida antes de convertir.

```
string entrada = Console.input(text="Edad: ")
if (es_numero_valido(entrada)) {
    int edad = int(entrada)
} else {
    Console.print("Debe ingresar un número")
}
```

2. O captura el error:

```
try {
    int edad = Console.input(text="Edad: ")
} catch (ErrorEntrada e) {
    Console.print("Entrada inválida, intente de nuevo")
}
```

3. Repite la petición hasta que el dato sea válido (bucle `do while`).

**Cómo evitarlo.** Indica en el mensaje el formato esperado (`"Ingrese su edad (número entero): "`) y valida o captura errores en toda entrada crítica.

---

## NX61: Archivo no encontrado

**Descripción.** Se intentó **leer, escribir, agregar o eliminar un archivo que no existe** en la ruta indicada. Se corresponde con `ErrorArchivo`.

**Causa común.** Escribir mal la ruta, olvidar crear el archivo antes, o usar una ruta relativa desde otro directorio.

**Ejemplo que lo genera.**

```
#inject file;

string contenido = file.read("datos_inexistentes.txt")   // NX61
```

**Solución paso a paso.**

1. Comprueba la ruta exacta.
2. Verifica la existencia antes de operar:

```
if (file.exists("datos.txt")) {
    string contenido = file.read("datos.txt")
} else {
    Console.print("El archivo no existe")
}
```

3. O captura el error con `try/catch` (`ErrorArchivo`).

**Cómo evitarlo.** Usa `file.exists(ruta)` antes de leer o eliminar. Para datos de prueba, garantiza que el archivo se cree (con `file.write`) antes de intentar leerlo.

---

## NX62: Error de lectura/escritura

**Descripción.** Una operación de `file` **no pudo completarse por una razón distinta a "no existe"**: permisos insuficientes, el archivo está bloqueado, el disco está lleno o la ruta es inválida. Se corresponde con `ErrorArchivo`.

**Causa común.** Escribir en un directorio sin permisos o intentar sobreescribir mientras el archivo está en uso.

**Ejemplo que lo genera.**

```
file.write("/root/datos_protegidos.txt", "contenido")   // NX62 sin permisos
```

**Solución paso a paso.**

1. Revisa los permisos de la ruta y el tipo de operación.
2. Asegúrate de que el directorio exista (`file.crear_directorio`) antes de escribir.
3. Captura el error para no abortar el programa:

```
try {
    file.write("salida.txt", contenido)
} catch (ErrorArchivo e) {
    Console.print("No se pudo guardar el archivo: " + e.mensaje())
}
```

**Cómo evitarlo.** Escribe siempre en rutas con permisos de escritura conocidos y crea los directorios antes de usarlos. Captura `ErrorArchivo` cuando la operación pueda fallar por el entorno.

---

## NX63: Directorio no encontrado al listar

**Descripción.** `file.listar_directorio(ruta)` recibió una **ruta que no existe o que no es un directorio**. No hay contenido que listar.

**Causa común.** Escribir mal la ruta o listar un archivo en lugar de un directorio.

**Ejemplo que lo genera.**

```
#inject file;

Vector<string> archivos = file.listar_directorio("carpeta_inexistente")   // NX63
```

**Solución paso a paso.**

1. Comprueba la ruta y que exista:

```
if (file.exists("carpeta")) {
    Vector<string> archivos = file.listar_directorio("carpeta")
}
```

2. O captura el error con `try/catch` (`ErrorArchivo`).

**Cómo evitarlo.** Verifica con `file.exists(ruta)` antes de listar y asegúrate de que el destino sea un directorio (y no un archivo).

---

# Categoría: Red y gráficos (NX70–NX79)

## NX70: Error de red

**Descripción.** Una petición HTTP o una conexión TCP de la librería `network` **no pudo completarse**: URL inválida, servidor inalcanzable, tiempo de espera agotado o respuesta no válida. Se corresponde con `ErrorRed`.

**Causa común.** Falta de conexión, la URL está mal escrita o el servidor no responde.

**Ejemplo que lo genera.**

```
#inject network;

auto respuesta = network.get("https://servidor.invalido.xyz")   // NX70
```

**Solución paso a paso.**

1. Verifica la URL (protocolo, dominio, ruta).
2. Comprueba la conexión a internet.
3. Captura el error y prueba reintentar:

```
try {
    auto respuesta = network.get(url)
    Console.print(respuesta.estado)
} catch (ErrorRed e) {
    Console.print("No se pudo conectar: " + e.mensaje())
}
```

**Cómo evitarlo.** Valida las URLs antes de usarlas, configura tiempos de espera y considera que la red puede fallar: captura `ErrorRed` en toda operación de red.

---

## NX71: Error gráfico

**Descripción.** Una operación de la librería `graphics` falló: no se pudo crear la ventana, el color es inválido o se dibujó fuera de la ventana.

**Causa común.** Usar un nombre de color no soportado o coordenadas fuera de los límites de la ventana.

**Ejemplo que lo genera.**

```
#inject graphics;

graphics.crear_ventana(800, 600, "Demo")
graphics.rectangulo(-50, 0, 100, 50, "color_no_existe")   // NX71
```

**Solución paso a paso.**

1. Revisa los argumentos (coordenadas, tamaños, colores válidos).
2. Asegúrate de que la ventana exista antes de dibujar (`crear_ventana` primero).
3. Captura el error:

```
try {
    graphics.rectangulo(100, 100, 200, 120, "azul")
} catch (ErrorGrafico e) {
    Console.print("No se pudo dibujar: " + e.mensaje())
}
```

**Cómo evitarlo.** Usa siempre colores y coordenadas válidos y crea la ventana antes de dibujar.

---

# Categoría: Módulos e importación (NX80–NX89)

## NX80: Módulo no encontrado

**Descripción.** La directiva `#inject` intentó importar una **librería nativa o un archivo local que no existe**. La librería `math` no está entre las nativas, o la ruta `"carpeta/archivo.nex"` no se encuentra.

**Causa común.** Escribir mal el nombre de la librería o la ruta del archivo.

**Ejemplo que lo genera.**

```
#inject mate;       // NX80: no existe la librería 'mate'
#inject "no_existe.nex";   // NX80: el archivo no existe
```

**Solución paso a paso.**

1. Revisa el nombre: las librerías nativas son `math`, `string`, `vector`, `stack`, `queue`, `set`, `map`, `linked_list`, `tree`, `graph`, `trie`, `file`, `time`, `random`, `graphics`, `network`.
2. Revisa la ruta del archivo local: debe existir en esa posición relativa al programa.
3. Corrige el nombre o la ruta.

```
#inject math;
#inject "utilidades/calculos.nex";
```

**Cómo evitarlo.** Consulta el catálogo de librerías antes de importar y mantén tus archivos propios en carpetas conocidas con nombres coincidentes.

---

## NX81: Importación circular

**Descripción.** Dos o más archivos se **importan entre sí de forma circular** (A importa a B, y B importa a A). Nexis no puede resolver el orden de importación sin caer en un bucle infinito.

**Causa común.** Diseñar dependencias cruzadas entre módulos.

**Ejemplo que lo genera.**

```
// a.nex
#inject "b.nex";
FuncionDeB()

// b.nex
#inject "a.nex";   // NX81: importación circular
FuncionDeA()
```

**Solución paso a paso.**

1. Identifica el ciclo: `a → b → a`.
2. Extrae las funciones compartidas a un tercer módulo `comun.nex`.
3. Haz que `a.nex` y `b.nex` importen solo `comun.nex`, eliminando el ciclo.

```
// comun.nex: define las funciones compartidas
// a.nex: #inject "comun.nex";
// b.nex: #inject "comun.nex";
```

**Cómo evitarlo.** Diseña módulos con una única dirección de dependencia (de abajo hacia arriba) y evita importaciones mutuas. Un módulo "base" común rompe los ciclos.

---

## NX82: Función usada sin importar

**Descripción.** Se llamó a una **función de una librería o módulo que no se importó** con `#inject`. También aplica cuando dos librerías importadas exponen la **misma función** y no se puede saber a cuál te refieres.

**Causa común.** Usar `math.sqrt` sin haber hecho `#inject math;`, o usar una función ambigua de dos módulos.

**Ejemplo que lo genera.**

```
float r = math.sqrt(81)   // NX82: falta #inject math;
```

**Solución paso a paso.**

1. Agrega la importación al inicio del archivo.

```
#inject math;

float r = math.sqrt(81)
```

2. Si la ambigüedad viene de dos módulos con la misma función, califica la llamada con el nombre del módulo (`matematica.perimetro()`) o importa con alias (si el lenguaje lo permite en la versión final).

**Cómo evitarlo.** Verifica que cada librería que usas esté importada. Mantén tus funciones propias en módulos con nombres que eviten colisiones.

---

## NX83: Extensión de archivo inválida en `#inject`

**Descripción.** `#inject "ruta/archivo.txt"` intentó importar un archivo **que no tiene extensión `.nex`**. Los módulos propios de Nexis son archivos `.nex`.

**Causa común.** Importar por error un `.txt`, `.json` o un archivo sin extensión.

**Ejemplo que lo genera.**

```
#inject "utilidades/datos.txt";   // NX83: los módulos propios se guardan con extensión .nex
```

**Solución paso a paso.**

1. Renombra el archivo a `.nex` y corrige la ruta:

```
#inject "utilidades/datos.nex";
```

**Cómo evitarlo.** Guarda tus librerías con extensión `.nex` y escribe siempre la ruta completa con esa extensión.

---

## NX84: Símbolo no encontrado en el módulo importado

**Descripción.** Se llamó `modulo.nombre()` y **`nombre` no está definido en el módulo** importado con `#inject`. El módulo no expone ese símbolo (función, clase o constante).

**Causa común.** Escribir mal el nombre de la función, o llamar a una función que pertenece a otro módulo.

**Ejemplo que lo genera.**

```
#inject "geometria.nex";

float area = geometria.areaCirculo(5)   // NX84 si 'areaCirculo' no está en geometria.nex
```

**Solución paso a paso.**

1. Comprueba qué define exactamente `geometria.nex` (funciones, clases, constantes).
2. Corrige el nombre o importa el módulo correcto.

**Cómo evitarlo.** Mantén un inventario de las funciones que expone cada módulo propio y califica las llamadas con el nombre correcto del módulo.

---

# Categoría: Sintaxis y sistema (NX90–NX99)

## NX90: Error de sintaxis

**Descripción.** La estructura del código **no respeta la gramática de Nexis**: llaves sin cerrar, paréntesis incompletos, palabras clave mal escritas o sentencias fuera de lugar.

**Causa común.** Escribir a mano rápido, copiar fragmentos con estilos mezclados o una llave extra/faltante.

**Ejemplo que lo genera.**

```
if (edad >= 18 {   // NX90: falta el paréntesis de cierre
    Console.print("Mayor")
}
```

**Solución paso a paso.**

1. Revisa la línea que indica el compilador.
2. Cuenta llaves `{}`, paréntesis `()` y corchetes `[]` abiertos y cerrados.
3. Comprueba que las palabras clave estén bien escritas (`if`, `else`, `while`, `for`, `func`, `void`).
4. No mezcles estilos de bloques: usa llaves o dos puntos (`:`), pero no ambos en la misma estructura.

```
if (edad >= 18) {
    Console.print("Mayor")
}
```

**Cómo evitarlo.** Usa el resaltado de sintaxis del editor de Nexis para detectar estilos mezclados, y escribe las estructuras completas antes de rellenar su cuerpo.

---

## NX91: Comentario o cadena mal cerrada

**Descripción.** Un **comentario de bloque o una cadena de texto no se cerró** antes de terminar el archivo o la línea. Nexis queda esperando el cierre.

**Causa común.** Olvidar el cierre `#/* ... */#` o `/* ... */`, o una comilla `"` sin pareja en un `string`.

**Ejemplo que lo genera.**

```
#/*
bloque sin cerrar
```   // NX91: falta */#

string saludo = "Hola, mundo   // NX91: falta la comilla de cierre
```

**Solución paso a paso.**

1. Completa el bloque o la cadena.

```
#/*
bloque cerrado correctamente
*/#

string saludo = "Hola, mundo"
```

2. Para comentarios de una línea usa `#/` y para bloques `#/* ... */#` (o `/* ... */`).

**Cómo evitarlo.** Cierra cada cadena con su comilla al mismo tiempo que la abres (los editores suelen autocompletar), y escribe los comentarios de bloque con ambos delimitadores desde el inicio.

---

## NX92: Desbordamiento de pila o memoria

**Descripción.** La ejecución se quedó **sin memoria**: recursión sin caso base, colecciones que crecen sin límite en un bucle o arreglos demasiado grandes. Se corresponde con `ErrorMemoria`.

**Causa común.** Llamar a una función recursiva sin condición de parada (por ejemplo, Fibonacci recursivo sin caso base).

**Ejemplo que lo genera.**

```
func recursiva() -> int {
    recursiva()   // NX92: se llama a sí misma sin caso base
}
```

**Solución paso a paso.**

1. Completa el caso base de la recursión.

```
func factorial(int: n) -> int {
    if n <= 1 {
        emit -> 1
    } else {
        emit -> n * factorial(n - 1)
    }
}
```

2. Si el problema es una colección infinita, valida las condiciones de parada del bucle.
3. Si necesitas procesar mucha información, prefiere versiones iterativas sobre recursivas.

**Cómo evitarlo.** Toda función recursiva debe tener un caso base alcanzable. Prefiere bucles cuando la profundidad pueda ser grande, y controla el crecimiento de colecciones dentro de bucles.

---

## NX99: Error interno del lenguaje

**Descripción.** Error **no previsto por la versión demo de Nexis**: la documentación no lo cubre y normalmente se trata de un fallo del intérprete. No es la causa de tu código, sino un inconveniente de la herramienta.

**Causa común.** Una combinación de construcciones poco habitual que la versión v0.0.1 no contempla, o un estado inválido del intérprete.

**Ejemplo.** Un mensaje con el código `NX99` acompañado de un reporte del intérprete.

**Solución paso a paso.**

1. Guarda el programa y el mensaje de error completo.
2. Intenta reformular el fragmento con construcciones simples (divide el problema en partes).
3. Reporta el caso con el código que lo genera y la versión del lenguaje, idealmente en el repositorio oficial del proyecto.

**Cómo evitarlo.** Mantente en las construcciones documentadas de la versión demo. Si aparece `NX99`, reportarlo ayuda a mejorar la próxima versión.

---

- Anterior: [Manejo de errores y colecciones (NX40–NX59)](catalog-03-errores-y-colecciones.md)
- [Volver al índice de errores](errors.md)
