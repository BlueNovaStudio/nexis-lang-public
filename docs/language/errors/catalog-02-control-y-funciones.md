# Catálogo de errores: Control de flujo y funciones (NX20–NX39)

Parte del [catálogo de errores de Nexis](errors.md). Cada código
incluye descripción, causa, ejemplo, solución paso a paso y cómo
evitarlo.

# Categoría: Control de flujo (NX20–NX29)

## NX20: `break` fuera de un bucle

**Descripción.** Se usó la palabra clave `break` **fuera de un bucle** (`while`, `do while`, `for`, `foreach`) o de un `switch`. `break` solo tiene sentido para salir de estas estructuras.

**Causa común.** Copiar un `break` de un bloque `witch`/bucle a un `if` suelto, o dejar un `break` después de cerrar el bucle.

**Ejemplo que lo genera.**

```
break   // NX20: break fuera de un bucle o switch
```

**Solución paso a paso.**

1. Verifica si la palabra está dentro de un bucle o `switch`.
2. Si es un `if` suelto, revisa si el `if` está a su vez dentro de un bucle (en ese caso está bien).
3. Si no, elimina el `break` o muévelo a su lugar correcto dentro del bloque.

```
for i in 0 .. 10 {
    if (i == 5) {
        break   // ok: está dentro del for
    }
}
```

**Cómo evitarlo.** Mantén `break`/`continue` únicamente dentro de bucles y `switch`. Antes de escribir `break`, confirma que el bloque contenedor inmediato sea un bucle o `switch`.

---

## NX21: `continue` fuera de un bucle

**Descripción.** Se usó `continue` **fuera de un bucle**. `continue` salta a la siguiente iteración, por lo que solo puede estar dentro de `while`, `do while`, `for` o `foreach`.

**Causa común.** Colocar `continue` en un `if` que no está dentro de ningún bucle, o usarlo dentro de un `switch` equivocadamente.

**Ejemplo que lo genera.**

```
continue   // NX21: continue fuera de un bucle
```

**Solución paso a paso.**

1. Confirma que el `continue` esté dentro de un bucle.
2. Si está dentro de un `switch` y quieres saltar el resto del `switch`, usa `break`.
3. Mueve el `continue` al interior del bucle.

```
for i in 0 .. 5 {
    if (i == 2) {
        continue   // ok: dentro del for
    }
    Console.print(i)
}
```

**Cómo evitarlo.** Usa `break` para salir de `switch` y `continue` solo para saltar iteraciones de bucles.

---

## NX22: Paso de bucle inválido

**Descripción.** Se definió un bucle `for` con un **paso (`step`) igual a cero** (o inválido). Con paso `0` el bucle nunca avanzaría y sería un bucle infinito instantáneo.

**Causa común.** Calcular el paso con una variable que puede valer `0`, o escribir `step 0` por error.

**Ejemplo que lo genera.**

```
for i in 0 .. 10 step 0 {   // NX22: el paso no puede ser cero
    Console.print(i)
}
```

**Solución paso a paso.**

1. Revisa el valor del paso.
2. Asegúrate de que sea distinto de cero. Un paso negativo hace que el rango se recorra en orden inverso; un paso positivo, en orden normal.
3. Si el paso viene de una variable, valídalo:

```
int paso = Console.input(text="Paso: ")
if (paso != 0) {
    for i in 0 .. 10 step paso {
        Console.print(i)
    }
}
```

**Cómo evitarlo.** Nunca escribas `step 0`. Si el paso depende de datos, verifica que no sea `0` antes de entrar al bucle.

---

## NX23: Condición no booleana

**Descripción.** Se usó una **condición que no es `bool`** en un `if`, `while`, `do while` o en el operador ternario `=>`. La condición debe ser `true` o `false`; Nexis no interpreta números o textos como verdadero/falso de forma implícita.

**Causa común.** Escribir `if (5)`, `if (texto)` o comparar con un solo `=` (asignación) en lugar de `==`.

**Ejemplo que lo genera.**

```
if (5) {   // NX23: 5 no es un valor booleano
    Console.print("Siempre?")
}
```

**Solución paso a paso.**

1. Cambia la condición por una comparación o expresión booleana.

```
int edad = 20
if (edad >= 18) {   // edad >= 18 es bool
    Console.print("Mayor de edad")
}
```

2. Si escribiste `=` en lugar de `==`, corrígelo.

```
if (edad == 18) { ... }   // comparación
```

**Cómo evitarlo.** Escribe siempre condiciones con operadores de comparación (`==`, `!=`, `>`, `<`, `>=`, `<=`) o lógicos (`&&`, `||`, `!`). No uses asignación `=` dentro de una condición.

---

## NX24: Caso duplicado en `switch`

**Descripción.** Un `switch` tiene **dos o más `case` con el mismo valor**. Después de la primera coincidencia sería imposible decidir qué bloque ejecutar.

**Causa común.** Copiar casos, o usar valores que por conversión terminan siendo iguales.

**Ejemplo que lo genera.**

```
switch (dia) {
    case 1:
        Console.print("Lunes")
    break
    case 1:   // NX24: caso 1 duplicado
        Console.print("Otro")
    break
}
```

**Solución paso a paso.**

1. Revisa todos los `case` buscando valores repetidos.
2. Une los casos repetidos o elimina el duplicado.
3. Para valores consecutivos usa rangos `case 90 ... 100:`.

```
switch (calificacion) {
    case 90 ... 100:
        Console.print("Excelente")
    break
    default:
        Console.print("Regular")
}
```

**Cómo evitarlo.** Lleva un orden en los `case` (por valor) y revisa la lista antes de agregar uno nuevo. Usa rangos `...` en vez de listar cada valor.

---

## NX25: `case` o `default` fuera de `switch`

**Descripción.** Se escribió `case` o `default` **fuera del cuerpo de un `switch`**. Estas palabras clave solo tienen sentido dentro de la estructura `switch`.

**Causa común.** Pegar `case` de un `switch` anterior, o escribir `default:` suelto.

**Ejemplo que lo genera.**

```
case 1:   // NX25: case fuera de un switch
    Console.print("Uno")
```

**Solución paso a paso.**

1. Mueve el `case`/`default` dentro de un `switch`:

```
switch (opcion) {
    case 1:
        Console.print("Uno")
    break
}
```

2. Si sobraba, elimínalo.

**Cómo evitarlo.** Escribe el `switch` completo con sus `case` dentro; no copies líneas sueltas de `case`.

---

## NX26: `default` duplicado en `switch`

**Descripción.** Un mismo `switch` tiene **dos o más bloques `default`**. El comportamiento "cuando ningún `case` coincide" solo puede definirse una vez.

**Causa común.** Copiar un bloque y olvidar eliminar el `default` original.

**Ejemplo que lo genera.**

```
switch (opcion) {
    case 1:
    break
    default:
    default:   // NX26: default duplicado
}
```

**Solución paso a paso.**

1. Conserva un único `default`, normalmente al final del `switch`.
2. Elimina los demás.

**Cómo evitarlo.** Revisa que tu `switch` contenga un solo `default`, al final, después de todos los `case`.

---

## NX27: Rango de `case` invertido

**Descripción.** En un rango de `case` (sintaxis `case A ... B:`) el **inicio es mayor que el fin**: `case 30 ... 3:`. El rango no contiene ningún valor.

**Causa común.** Escribir el rango en orden inverso por error.

**Ejemplo que lo genera.**

```
switch (calificacion) {
    case 30 ... 3:   // NX27: el rango está invertido (debe ser 3 ... 30)
}
```

**Solución paso a paso.**

1. Escribe el rango de menor a mayor:

```
switch (calificacion) {
    case 3 ... 30:
}
```

**Cómo evitarlo.** Los rangos de `case` siempre van de menor a mayor (`A ... B` con `A <= B`).

---

## NX28: Valor de `case` con tipo distinto al del `switch`

**Descripción.** Un `case` usa un **valor de tipo distinto** al de la expresión evaluada por el `switch`. Todos los `case` deben coincidir con el tipo de la expresión.

**Causa común.** `switch (nombre)` con `case 3:` en lugar de `case "guardar":`.

**Ejemplo que lo genera.**

```
switch (comando) {   // comando es string
    case 3:          // NX28: case int en un switch de string
}
```

**Solución paso a paso.**

1. Comprueba el tipo de la expresión del `switch`.
2. Escribe los `case` con ese mismo tipo:

```
switch (comando) {
    case "guardar":
}
```

**Cómo evitarlo.** Usa valores del mismo tipo en la expresión y en todos los `case` dentro de cada `switch`.

---

## NX29: Límites o paso del `for` no numéricos

**Descripción.** En un `for` con rango (`for i in a .. b`) el **inicio, el fin o el `step` no son números enteros**. El rango y el paso deben poder evaluarse como enteros.

**Causa común.** `for i in 0 .. "10"` o `for i in 0 .. 10 step "2"`.

**Ejemplo que lo genera.**

```
for i in 0 .. "5" {   // NX29: el límite debe ser un entero
    Console.print(i)
}
```

**Solución paso a paso.**

1. Convierte o corrige los límites/paso:

```
int limite = int("5")
for i in 0 .. limite {
    Console.print(i)
}
```

**Cómo evitarlo.** El rango `a .. b` y el `step` siempre son enteros; conviértelos antes de usarlos si vienen de `Console.input`.

---

# Categoría: Funciones (NX30–NX39)

## NX30: Ruta sin retorno en función

**Descripción.** Una función que declara un tipo de retorno (`func ... -> tipo`) tiene **al menos una ruta de ejecución que no devuelve ningún valor**. Por ejemplo, un `if` que retorna y un `else` que no.

**Causa común.** Olvidar el `emit ->` o el retorno implícito en una de las ramas.

**Ejemplo que lo genera.**

```
func es_par(int: numero) -> bool {
    if numero % 2 == 0 {
        emit -> true
    }
    // falta el retorno cuando es impar → NX30
}
```

**Solución paso a paso.**

1. Recorre todos los caminos de la función (if/else, switch, bucles).
2. Asegúrate de que **cada camino** termine en `emit -> valor` o en un retorno implícito.
3. Añade el retorno que falta:

```
func es_par(int: numero) -> bool {
    if numero % 2 == 0 {
        emit -> true
    } else {
        emit -> false
    }
}
```

**Cómo evitarlo.** Diseña las funciones de modo que haya una sola expresión de salida al final, o que todas las ramas retornen. Después de escribir una función con `if/else`, verifica que ambos lados tengan `emit ->`.

---

## NX31: Falta tipo de retorno

**Descripción.** Una función `func` **no declara el tipo que devuelve** (falta `-> tipo`) o usa `->` sin tipo. Si no devuelve nada, debe declararse como `void`; si devuelve algo, debe indicarlo.

**Causa común.** Escribir `func suma(...) { a + b }` olvidando `-> int`.

**Ejemplo que lo genera.**

```
func suma(int: a, int: b) {   // NX31: falta -> int
    a + b
}
```

**Solución paso a paso.**

1. Decide qué devuelve la función.
2. Si devuelve un valor, agrega el tipo tras `->`:

```
func suma(int: a, int: b) -> int {
    a + b
}
```

3. Si no devuelve nada, escribe `void`:

```
void mostrar_suma(int: a, int: b) {
    Console.print(a + b)
}
```

**Cómo evitarlo.** Declara siempre el tipo de retorno. Usa `func nombre(...) -> tipo` para funciones que devuelven valor y `void nombre(...)` para procedimientos.

---

## NX32: Cantidad de argumentos incorrecta

**Descripción.** Al **llamar una función se pasaron más o menos argumentos** de los que declara su firma.

**Causa común.** Cambiar la firma de una función (agregar/quitar parámetros) y olvidar actualizar las llamadas.

**Ejemplo que lo genera.**

```
func suma(int: a, int: b) -> int {
    a + b
}

int r = suma(5)          // NX32: faltan argumentos (se esperaban 2)
int r2 = suma(1, 2, 3)   // NX32: sobran argumentos (se esperaban 2)
```

**Solución paso a paso.**

1. Cuenta los parámetros declarados en la firma.
2. Cuenta los argumentos en cada llamada.
3. Iguala la cantidad. Si la función admite valores por defecto (`int: edad = 18`), esos parámetros se pueden omitir:

```
int r = suma(5, 3)   // ok
```

**Cómo evitarlo.** Antes de llamar a una función, revisa su firma. Si agregas parámetros nuevos, usa un valor por defecto para no romper llamadas existentes.

---

## NX33: Tipo de argumento incorrecto

**Descripción.** Se pasó a una función un **argumento cuyo tipo no coincide** con el parámetro declarado.

**Causa común.** Enviar un `string` donde se espera `int`, o un `float` donde se espera `bool`.

**Ejemplo que lo genera.**

```
func multiplicar(int: a, int: b) -> int {
    a * b
}

int r = multiplicar("x", 3)   // NX33: se esperaba int, se recibió string
```

**Solución paso a paso.**

1. Revisa el tipo de cada parámetro en la firma.
2. Convierte el argumento al tipo esperado, o cambia la firma si el diseño fue incorrecto.

```
string valor = "3"
int r = multiplicar(int(valor), 3)   // ok
```

**Cómo evitarlo.** Mantén los tipos consistentes entre la firma y las llamadas. Al leer entradas, especifica el tipo (`int x = Console.input(...)`) para que coincida con lo que espera la función.

---

## NX34: Función declarada dos veces

**Descripción.** Se definió **la misma función con el mismo nombre** más de una vez en el mismo ámbito. Nexis (versión demo) no permite sobrecarga: el nombre de función debe ser único.

**Causa común.** Copiar la definición de una función, o importar dos módulos que exponen una función con el mismo nombre (ver [NX82](catalog-04-io-modulos-y-sistema.md#nx82-función-usada-sin-importar)).

**Ejemplo que lo genera.**

```
func duplicar(int: x) -> int {
    x * 2
}

func duplicar(int: y) -> int {   // NX34: la función 'duplicar' ya existe
    y * 2
}
```

**Solución paso a paso.**

1. Localiza las dos definiciones.
2. Elimina la duplicada o renómbrala con un nombre distinto.

```
func duplicar(int: x) -> int {
    x * 2
}
```

**Cómo evitarlo.** Usa nombres descriptivos y únicos para cada función. Si dos módulos importados definen la misma función, usa alias o renombra al importar (ver [NX82](catalog-04-io-modulos-y-sistema.md#nx82-función-usada-sin-importar)).

---

## NX35: Parámetro repetido en la firma

**Descripción.** Una misma función tiene **dos parámetros con el mismo nombre**. No se puede distinguir cuál es cuál dentro del cuerpo.

**Causa común.** Copiar parámetros al definir la firma.

**Ejemplo que lo genera.**

```
func sumar(int: a, int: a) -> int {   // NX35: parámetro repetido 'a'
    a + a
}
```

**Solución paso a paso.**

1. Renombra los parámetros repetidos con nombres únicos.

```
func sumar(int: a, int: b) -> int {
    a + b
}
```

**Cómo evitarlo.** Al definir una función, revisa que cada parámetro tenga un nombre distinto y único dentro de la firma.

---

## NX36: `emit` en función `void`

**Descripción.** Se usó `emit -> valor` **dentro de una función declarada como `void`**. Una función `void` no devuelve valor, por lo que no puede emitir nada.

**Causa común.** Convertir una función con retorno a `void` y olvidar eliminar sus `emit`.

**Ejemplo que lo genera.**

```
void mostrar() {
    emit -> 5   // NX36: void no puede emitir un valor
}
```

**Solución paso a paso.**

1. Elimina el `emit` y deja la lógica directamente:

```
void mostrar() {
    Console.print(5)
}
```

2. Si la función SÍ debe devolver un valor, cambia `void` por `func ... -> tipo`:

```
func dame_cinco() -> int {
    emit -> 5
}
```

**Cómo evitarlo.** Decide antes: `void` = no devuelve nada (sin `emit`); `func ... -> tipo` = devuelve valor (con `emit ->`).

---

## NX37: `emit` fuera de una función

**Descripción.** Se escribió `emit -> valor` **fuera de una función o método**. Solo dentro de una función (`func`/`void`) tiene sentido emitir un valor.

**Causa común.** Pegar el `emit` de una función al nivel principal del programa.

**Ejemplo que lo genera.**

```
emit -> 10   // NX37: emit fuera de una función
```

**Solución paso a paso.**

1. Envuelve el código en una función si pertenece a una:

```
func configurar() -> int {
    emit -> 10
}
```

2. O usa una asignación directamente:

```
int x = 10
```

**Cómo evitarlo.** `emit` solo aparece dentro del cuerpo de `func`/`void`. Fuera, usa variables y sentencias normales.

---

---

- Anterior: [Variables, constantes y tipos (NX00–NX19)](catalog-01-variables-y-tipos.md)
- Siguiente: [Manejo de errores y colecciones (NX40–NX59)](catalog-03-errores-y-colecciones.md)
- [Volver al índice de errores](errors.md)
