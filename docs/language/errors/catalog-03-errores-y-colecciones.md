# Catálogo de errores: Manejo de errores y colecciones (NX40–NX59)

Parte del [catálogo de errores de Nexis](errors.md). Cada código
incluye descripción, causa, ejemplo, solución paso a paso y cómo
evitarlo.

# Categoría: Manejo de errores (NX40–NX49)

## NX40: `catch` sin `try` previo

**Descripción.** Se escribió un bloque `catch` (o `finally`) **sin un `try` que lo acompañe**. Las excepciones solo se capturan dentro de la estructura `try/catch/finally`.

**Causa común.** Pegar un `catch` suelto o borrar el `try` por accidente.

**Ejemplo que lo genera.**

```
catch (Error e) {   // NX40: catch sin try previo
    Console.print(e.mensaje())
}
```

**Solución paso a paso.**

1. Envuelve el código que puede fallar en un `try` y coloca el `catch` justo después.

```
try {
    int resultado = 10 / 0
} catch (Error e) {
    Console.print(e.mensaje())
}
```

**Cómo evitarlo.** Recuerda la estructura: `try { ... } catch (Tipo e) { ... } finally { ... }`. Siempre que veas `catch`, asegúrate de que exista el `try` inmediatamente anterior.

---

## NX41: `try` vacío

**Descripción.** Un bloque `try` **no contiene ninguna sentencia**. No hay código que pueda lanzar un error. Es señal de código incompleto.

**Causa común.** Crear la estructura `try/catch` antes de escribir el código que la necesita.

**Ejemplo que lo genera.**

```
try {
    // NX41: try vacío, no hay sentencias
} catch (Error e) {
    Console.print(e.mensaje())
}
```

**Solución paso a paso.**

1. Escribe el código que puede fallar dentro del `try`.

```
try {
    Vector<int> nums = [10, 20]
    int valor = nums.get(9)
} catch (ErrorIndice e) {
    Console.print(e.mensaje())
}
```

**Cómo evitarlo.** Escribe primero el código con su riesgo, y después decide qué `try/catch` lo protege. Un `try` vacío no aporta valor.

---

## NX42: Error no capturado

**Descripción.** Se lanzó una excepción **que ningún `catch` de la pila estaba preparado para manejar**. En la versión demo, esto **aborta la ejecución** del programa y muestra el código de error, el mensaje, la línea y el archivo donde ocurrió.

**Causa común.** No prever una operación que puede fallar (división por cero, índice fuera de rango, archivo inexistente) o capturar un tipo distinto al error lanzado.

**Ejemplo que lo genera.**

```
Vector<int> nums = [1, 2, 3]
Console.print(nums.get(8))   // NX42: error no capturado (ErrorIndice)
```

**Solución paso a paso.**

1. Lee el reporte: te indica el tipo de error y dónde ocurrió.
2. Envuelve la operación riesgosa en `try/catch`:

```
try {
    Vector<int> nums = [1, 2, 3]
    Console.print(nums.get(8))
} catch (ErrorIndice e) {
    Console.print("Posición inválida: " + e.mensaje())
}
```

3. O previene el error validando antes de la operación (compara el índice con `longitud()`).

**Cómo evitarlo.** Identifica qué operaciones de tu programa pueden fallar (índices, divisiones, archivos, red) y rodéalas con `try/catch` o valídalas. No dejes errores esperados sin manejar.

---

## NX43: Lanzar un valor que no es `Error`

**Descripción.** Se usó `lanzar` (o `throw`) con un valor que **no es un objeto de tipo `Error`** (o una de sus subclases), por ejemplo `lanzar 5` o `lanzar "mensaje"`. Solo se pueden lanzar errores.

**Causa común.** Confundir `lanzar` con un `print`, o lanzar un literal pensando que es válido.

**Ejemplo que lo genera.**

```
lanzar 5                  // NX43: 5 no es un Error
lanzar "ocurrió algo"     // NX43: un string no es un Error
```

**Solución paso a paso.**

1. Usa siempre una clase de error válida con su mensaje.

```
lanzar ErrorValidacion("El valor ingresado es inválido")
```

2. Si necesitas un error propio, define una clase que herede de `Error` (ver el capítulo de POO) o usa una de las clases documentadas (`ErrorIndice`, `ErrorDivision`, `ErrorTipo`, `ErrorEntrada`, `ErrorArchivo`, `ErrorRed`, `ErrorMemoria`, `ErrorValidacion`, `ErrorAssert`).

**Cómo evitarlo.** `lanzar` siempre recibe `ErrorTipo("mensaje")`, nunca literales directos. Revisa la tabla de tipos de error en [try_catch.md](try_catch.md).

---

## NX44: Aserción fallida

**Descripción.** La función `afirmar(condicion, mensaje)` se ejecutó y la **condición resultó falsa**. El programa detiene la ejecución con el mensaje indicado. Se corresponde con `ErrorAssert`.

**Causa común.** Una suposición sobre los datos no se cumple (por ejemplo, un vector que se creyó no vacío).

**Ejemplo que lo genera.**

```
afirmar(edad >= 0, "La edad no puede ser negativa")   // NX44 si edad < 0
```

**Solución paso a paso.**

1. Lee el mensaje: dice qué suposición se rompió.
2. Corrige la causa raíz (los datos o la lógica que los genera).
3. Para errores esperados (no invariantes), usa validación con `if` o `lanzar` en lugar de `afirmar`.

```
if (edad < 0) {
    lanzar ErrorValidacion("Edad inválida")
}
```

**Cómo evitarlo.** Usa `afirmar` solo para invariantes del programa (condiciones que SIEMPRE deben cumplirse). Para datos del usuario usa validación explícita.

---

## NX45: `catch` con tipo que no es `Error`

**Descripción.** El tipo declarado en `catch (Tipo e)` **no es `Error` ni una de sus subclases**. Solo se pueden capturar errores.

**Causa común.** Escribir `catch (int e)` o `catch (string valor)`.

**Ejemplo que lo genera.**

```
try {
    int resultado = 10 / 0
} catch (int e) {   // NX45: int no es un Error
    Console.print(e)
}
```

**Solución paso a paso.**

1. Usa `Error` o una subclase documentada (`ErrorDivision`, `ErrorIndice`, `ErrorTipo`, `ErrorArchivo`, ...). Consulta la tabla de la [guía de try/catch](try_catch.md).
2. Si necesitas capturar cualquier error, usa `Error`:

```
} catch (Error e) {
    Console.print(e.mensaje())
}
```

**Cómo evitarlo.** En los `catch`, el tipo siempre es `Error` o una clase que herede de `Error` (ver POO).

---

## NX46: `catch` sin variable

**Descripción.** Un bloque `catch` **no declaró la variable** que recibe el error: `catch (Error)` en lugar de `catch (Error e)`. Sin nombre no se puede acceder al error.

**Causa común.** Olvidar el nombre de la variable.

**Ejemplo que lo genera.**

```
try {
    int resultado = 10 / 0
} catch (ErrorDivision) {   // NX46: falta la variable (ErrorDivision e)
    Console.print("División inválida")
}
```

**Solución paso a paso.**

1. Añade el nombre de la variable:

```
} catch (ErrorDivision e) {
    Console.print(e.mensaje())
}
```

**Cómo evitarlo.** El patrón es siempre `catch (Tipo variable)`.

---

# Categoría: Colecciones (NX50–NX59)

## NX50: Operación sobre colección vacía

**Descripción.** Se intentó **extraer, leer o inspeccionar el primer/último elemento de una colección vacía**: `extraer()`, `desapilar()`, `desencolar()`, `cima()`, `frente()`, `primero()`, `ultimo()`.

**Causa común.** Olvidar verificar con `esta_vacia()`/`esta_vacio()` antes de consumir un elemento.

**Ejemplo que lo genera.**

```
Stack<int> pila = Stack()
int valor = pila.pop()   // NX50: la pila está vacía
```

**Solución paso a paso.**

1. Verifica el estado antes de operar.

```
if (!pila.isEmpty()) {
    int valor = pila.pop()
} else {
    Console.print("No hay elementos")
}
```

2. O captura la excepción con `try/catch`.

**Cómo evitarlo.** Antes de cada `pop`, `dequeue`, `pop`, `front`, `peek`, `first` o `last`, pregunta siempre si hay elementos. En bucles de consumo, la condición del bucle suele ser `while (!estructura.isEmpty())`.

---

## NX51: Modificar colección durante iteración

**Descripción.** Se intentó **agregar o eliminar elementos de una colección mientras se recorre** con `foreach` (o con un `for` basado en índices que cambia el tamaño). El comportamiento es indeterminado, por lo que Nexis lo rechaza.

**Causa común.** Eliminar elementos de un vector dentro de un `foreach` para "filtrarlos".

**Ejemplo que lo genera.**

```
foreach (numero in numeros) {
    if (numero < 0) {
        numeros.remove(indice)   // NX51: modificar durante la iteración
    }
}
```

**Solución paso a paso.**

1. Construye una **nueva colección** con los elementos que quieres conservar.
2. O recorre copiando primero la colección original.

```
Vector<int> filtrados = []
foreach (numero in numeros) {
    if (numero >= 0) {
        filtrados.add(numero)
    }
}
```

**Cómo evitarlo.** Nunca agregues ni elimines en la misma colección que estás recorriendo. Crea colecciones nuevas cuando necesites filtrar o transformar.

---

## NX52: Clave no encontrada en `Map`

**Descripción.** Se llamó `obtener(clave)` en un `Map<K, V>` con una **clave que no existe** en el mapa. No hay un valor asociado que devolver.

**Causa común.** Pedir una clave que nunca se guardó con `put`, o escribir mal el nombre de la clave.

**Ejemplo que lo genera.**

```
Map<string, int> inventario = {"manzanas": 50}
int cantidad = inventario.get("peras")   // NX52: la clave 'peras' no existe
```

**Solución paso a paso.**

1. Comprueba la existencia antes de obtener:

```
if (inventario.contains("peras")) {
    int cantidad = inventario.get("peras")
} else {
    inventario.put("peras", 0)
}
```

2. O captura el error con `try/catch`.

**Cómo evitarlo.** Antes de `obtener(clave)`, valida con `contiene(clave)` o inicializa la pareja con `put` si corresponde.

---

## NX53: Operación no soportada por la colección

**Descripción.** Se llamó un **método que la colección no implementa**: `desapilar()` en un `Vector`, `cima()` en un `Map`, etc. Cada estructura tiene su propio conjunto de métodos documentado.

**Causa común.** Aplicar la lógica de una pila a un vector sin cambiar los métodos.

**Ejemplo que lo genera.**

```
Vector<int> numeros = [1, 2, 3]
int ultimo = numeros.pop()   // NX53: Vector no tiene 'desapilar'
```

**Solución paso a paso.**

1. Revisa los métodos de la estructura en su capítulo (Vector, Stack, Queue, Set, Map, ...).
2. Usa el método correcto:

```
int ultimo = numeros.get(numeros.length() - 1)
```

3. Si necesitas el comportamiento de una pila, declara `Stack<int>` en su lugar.

**Cómo evitarlo.** Usa la estructura adecuada a la operación (pila → `Stack`, cola → `Queue`) y consulta el catálogo de métodos antes de llamarlos.

---

---

- Anterior: [Control de flujo y funciones (NX20–NX39)](catalog-02-control-y-funciones.md)
- Siguiente: [Entrada/salida, módulos, red y sistema (NX60–NX99)](catalog-04-io-modulos-y-sistema.md)
- [Volver al índice de errores](errors.md)
