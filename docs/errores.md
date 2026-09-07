# 🧩 Catálogo de errores de Nexis (códigos NX)

Este documento es la **referencia oficial de errores** de Nexis. Cada error tiene un código único con el formato `NXXX` para que sea fácil de buscar, reportar y resolver.

> **Cómo usar este catálogo:** busca el código `NXxx` en tu mensaje de error, ve a la sección correspondiente y sigue la solución paso a paso. Si el código no aparece, consulta la versión extendida en [language/errors/errors.md](language/errors/errors.md).

## Navegación rápida

- [Cómo funciona el sistema de errores](language/errors/README.md)
- [Manejo de excepciones (try/catch)](language/errors/try_catch.md)
- [Documentación principal](README.md)

---

## Tabla de códigos

| Código | Error | Categoría |
|--------|-------|-----------|
| [NX00](#nx00-variable-no-inicializada) | Variable no inicializada | Variables |
| [NX01](#nx01-división-por-cero) | División por cero | Variables |
| [NX02](#nx02-variable-no-definida) | Variable no definida | Variables |
| [NX03](#nx03-reasignación-de-constante) | Reasignación de constante | Variables |
| [NX04](#nx04-declaración-duplicada) | Declaración duplicada | Variables |
| [NX05](#nx05-identificador-inválido) | Identificador inválido | Variables |
| [NX06](#nx06-constante-sin-inicializar) | Constante sin inicializar | Variables |
| [NX07](#nx07-tipo-incompatible-en-asignación) | Tipo incompatible en asignación | Variables |
| [NX10](#nx10-operandos-con-tipos-incompatibles) | Operandos incompatibles | Tipos |
| [NX11](#nx11-índice-fuera-de-rango) | Índice fuera de rango | Tipos |
| [NX12](#nx12-conversión-de-tipo-inválida) | Conversión de tipo inválida | Tipos |
| [NX13](#nx13-operación-matemática-inválida) | Operación matemática inválida | Tipos |
| [NX20](#nx20-break-fuera-de-un-bucle) | `break` fuera de un bucle | Control de flujo |
| [NX21](#nx21-continue-fuera-de-un-bucle) | `continue` fuera de un bucle | Control de flujo |
| [NX22](#nx22-paso-de-bucle-inválido) | Paso de bucle inválido | Control de flujo |
| [NX23](#nx23-condición-no-booleana) | Condición no booleana | Control de flujo |
| [NX24](#nx24-caso-duplicado-en-switch) | Caso duplicado en `switch` | Control de flujo |
| [NX30](#nx30-ruta-sin-retorno-en-función) | Ruta sin retorno en función | Funciones |
| [NX31](#nx31-falta-tipo-de-retorno) | Falta tipo de retorno | Funciones |
| [NX32](#nx32-cantidad-de-argumentos-incorrecta) | Cantidad de argumentos incorrecta | Funciones |
| [NX33](#nx33-tipo-de-argumento-incorrecto) | Tipo de argumento incorrecto | Funciones |
| [NX34](#nx34-función-declarada-dos-veces) | Función declarada dos veces | Funciones |
| [NX35](#nx35-parámetro-repetido-en-la-firma) | Parámetro repetido en la firma | Funciones |
| [NX40](#nx40-catch-sin-try-previo) | `catch` sin `try` previo | Errores |
| [NX41](#nx41-try-vacío) | `try` vacío | Errores |
| [NX42](#nx42-error-no-capturado) | Error no capturado | Errores |
| [NX43](#nx43-lanzar-un-valor-que-no-es-error) | Lanzar un valor que no es `Error` | Errores |
| [NX44](#nx44-aserción-fallida) | Aserción fallida | Errores |
| [NX50](#nx50-operación-sobre-colección-vacía) | Operación sobre colección vacía | Colecciones |
| [NX51](#nx51-modificar-colección-durante-iteración) | Modificar colección durante iteración | Colecciones |
| [NX60](#nx60-formato-de-entrada-inválido) | Formato de entrada inválido | Entrada/Salida |
| [NX61](#nx61-archivo-no-encontrado) | Archivo no encontrado | Entrada/Salida |
| [NX62](#nx62-error-de-lectura-escritura) | Error de lectura/escritura | Entrada/Salida |
| [NX70](#nx70-error-de-red) | Error de red | Red |
| [NX71](#nx71-error-gráfico) | Error gráfico | Gráficos |
| [NX80](#nx80-módulo-no-encontrado) | Módulo no encontrado | Módulos |
| [NX81](#nx81-importación-circular) | Importación circular | Módulos |
| [NX82](#nx82-función-usada-sin-importar) | Función usada sin importar | Módulos |
| [NX90](#nx90-error-de-sintaxis) | Error de sintaxis | Sintaxis |
| [NX91](#nx91-comentario-o-cadena-mal-cerrada) | Comentario o cadena mal cerrada | Sintaxis |
| [NX92](#nx92-desbordamiento-de-pila-o-memoria) | Desbordamiento de pila o memoria | Sistema |
| [NX99](#nx99-error-interno) | Error interno del lenguaje | Sistema |

---

# Categoría: Variables y constantes (NX00–NX09)

## NX00: Variable no inicializada

**Descripción.** Se intentó **leer o usar una variable antes de asignarle un valor**. La variable existe y tiene tipo, pero todavía no tiene ningún valor almacenado. Nexis no permite leer una variable sin valor.

**Causa común.** Declarar con `tipo nombre;` y olvidar la asignación posterior, o declarar e intentar imprimir/operar en el mismo bloque de código.

**Ejemplo que lo genera.**

```
int contador;
Console.print(contador)   // NX00: la variable contador no ha sido inicializada
```

**Solución paso a paso.**

1. Ubica la línea del error indicada por el compilador.
2. Identifica la variable que no está inicializada (`contador`).
3. Busca en el código si se le asigna un valor antes de esa línea.
4. Si no existe la asignación, agrégala: `contador = 0`.
5. Si el valor se asigna dentro de un `if`, asegúrate de que **todas** las rutas la inicialicen.

```
int contador = 0
Console.print(contador)   // imprime 0
```

**Cómo evitarlo.** Acostúmbrate a inicializar en la misma línea (`int contador = 0`) o a asignar un valor inmediatamente después de declarar. Si usas `auto`, recuerda que exige inicialización en la misma línea.

---

## NX01: División por cero

**Descripción.** Se intentó dividir (operador `/`) u obtener el módulo (operador `%`) usando **cero como divisor**. En matemáticas y en Nexis, dividir entre cero no tiene un resultado definido.

**Causa común.** Ingresar un valor por teclado sin validarlo, o hacer una división cuyo denominador puede volverse `0` con ciertos datos.

**Ejemplo que lo genera.**

```
int a = 10
int b = 0
int resultado = a / b   // NX01: división por cero
```

**Solución paso a paso.**

1. Localiza la división o el módulo que falla.
2. Revisa de dónde viene el divisor (`b`): ¿entrada de usuario, resultado de un cálculo?
3. Valida el divisor antes de usarlo:

```
if (b != 0) {
    Console.print(a / b)
} else {
    Console.print("No se puede dividir entre cero")
}
```

4. También puedes capturarlo con `try/catch` y `ErrorDivision` (ver [NX42](#nx42-error-no-capturado)).

```
try {
    int resultado = a / b
} catch (ErrorDivision e) {
    Console.print("División inválida")
}
```

**Cómo evitarlo.** Nunca dividas sin comprobar antes que el divisor sea distinto de cero. Si el divisor proviene de una división entera como `(9 / 5)`, recuerda que en Nexis dividir enteros da un entero: usa `9.0 / 5` si necesitas decimales.

---

## NX02: Variable no definida

**Descripción.** Se usó un **identificador que no ha sido declarado** en ningún ámbito visible: no existe una variable (ni constante, ni función, ni tipo) con ese nombre. Es distinto de [NX00](#nx00-variable-no-inicializada): aquí la variable no existe; en NX00 existe pero sin valor.

**Causa común.** Escribir mal el nombre, olvidar declarar, usar la variable fuera de su ámbito (scope) o confundir nombres con mayúsculas/minúsculas distintas.

**Ejemplo que lo genera.**

```
edad = 18        // NX02: la variable 'edad' no ha sido declarada
Console.print(edades)   // NX02: además está mal escrita
```

**Solución paso a paso.**

1. Anota el nombre exacto del identificador del mensaje de error.
2. Revisa que esté **declarado antes** de su uso (`int edad = 18`).
3. Comprueba el ámbito: si se declaró dentro de un bloque `{ }` o de una función, no es visible fuera de él.
4. Verifica mayúsculas/minúsculas: `Edad`, `EDAD` y `edad` son identificadores distintos.
5. Si la variable debe ser global, muévela a la parte superior del archivo.

```
int edad = 18
Console.print(edad)   // ok
```

**Cómo evitarlo.** Declara siempre antes de usar, usa nombres consistentes en minúsculas con `snake_case` y mantén las variables en el ámbito más pequeño posible.

---

## NX03: Reasignación de constante

**Descripción.** Se intentó **modificar el valor de una constante** declarada con `const`. Las constantes solo pueden recibir valor en el momento de su declaración; cualquier asignación posterior es ilegal.

**Causa común.** Usar `const` para algo que luego se necesita cambiar, o copiar/pegar código donde una variable normal se convirtió en constante.

**Ejemplo que lo genera.**

```
const int x = 3
x = 4   // NX03: las constantes no pueden ser modificadas
```

**Solución paso a paso.**

1. Decide si el valor debe poder cambiar.
2. Si **no debe cambiar**, elimina la asignación posterior:

```
const int x = 3
Console.print(x)
```

3. Si **sí debe cambiar**, cambia la declaración a variable normal:

```
int x = 3
x = 4
Console.print(x)
```

**Cómo evitarlo.** Usa `const` solo para valores que permanecen fijos durante todo el programa (como `PI`, `GRAVEDAD`, `DIAS_SEMANA`), y usa `int`, `float`, etc. para valores que cambian.

---

## NX04: Declaración duplicada

**Descripción.** Se declaró **dos variables con el mismo nombre en el mismo ámbito (bloque)**. Nexis no permite redefinir un identificador en el mismo bloque porque sería ambiguo saber cuál usar.

**Causa común.** Copiar líneas de declaración al pegar código, o declarar la misma variable en dos lugares del mismo bloque por error.

**Ejemplo que lo genera.**

```
int x = 5
int x = 10   // NX04: ya existe una variable 'x' en este ámbito
```

**Solución paso a paso.**

1. Ubica la segunda declaración del mismo nombre.
2. Si quieres actualizar el valor, **elimina el tipo** y usa solo asignación:

```
int x = 5
x = 10   // asigna, no redeclara
```

3. Si eran variables distintas, renombra una de ellas con un nombre descriptivo.

```
int x = 5
int y = 10
```

**Cómo evitarlo.** Antes de declarar, revisa si el identificador ya existe en el bloque. Usa nombres descriptivos que no se repitan (`contador`, `total`, `promedio`). Recuerda: bloques internos `{ }` pueden declarar sus propias variables sin que esto sea un error.

---

## NX05: Identificador inválido

**Descripción.** Se usó un **nombre de variable, función o tipo con caracteres no permitidos** por las convenciones de Nexis. Los identificadores solo pueden contener letras (a–z, A–Z), números (0–9) y el guion bajo (`_`), y **no pueden empezar con un número**. No se permiten tildes, `ñ`, espacios ni símbolos.

**Causa común.** Escribir nombres como `número`, `correoñ` o `2da_opcion`, o usar guiones (`mi-variable`) en lugar de guiones bajos (`mi_variable`).

**Ejemplo que lo genera.**

```
int númer o = 5        // NX05: tilde y espacio no permitidos
int mañana = 1         // NX05: la ñ no está permitida
int 2da_opcion = 10    // NX05: no puede empezar con número
```

**Solución paso a paso.**

1. Escribe el identificador usando solo caracteres de la convención general (inglesa).
2. Reemplaza tildes y `ñ` por su equivalente sin acento o por su traducción al inglés.
3. Asegúrate de que **no comience con un dígito** y que use `_` en lugar de espacios o guiones.

```
int numero = 5         // ok
int manana = 1         // ok (o: int tomorrow = 1)
int segunda_opcion = 10   // ok
```

**Cómo evitarlo.** Nombra tus variables en inglés o en español **sin acentos ni `ñ`**, usa `snake_case` y empieza siempre con una letra o `_`.

---

## NX06: Constante sin inicializar

**Descripción.** Se declaró una constante con `const` **sin asignarle un valor** en la misma línea. A diferencia de las variables normales, una constante está obligada a tener valor desde el momento de su declaración.

**Causa común.** Declarar primero e intentar asignar después, imitando el patrón de las variables:

```
const double PI;    // NX06: constante sin inicializar
PI = 3.14159
```

**Solución paso a paso.**

1. Mueve la asignación dentro de la declaración.
2. Deja una sola línea con declaración e inicialización:

```
const double PI = 3.14159
```

3. Si el valor se conoce más adelante (por ejemplo, tecleado por el usuario), esa constante en realidad no es constante: usa `double` normal.

**Cómo evitarlo.** Siempre combina `const` + tipo + nombre + `=` + valor en una sola sentencia. Si no conoces el valor al declarar, no uses `const`.

---

## NX07: Tipo incompatible en asignación

**Descripción.** Se intentó **asignar un valor de un tipo distinto al declarado** sin una conversión válida. Nexis es un lenguaje con tipado estático: una vez que una variable es `int`, no puede guardar un `string`, y viceversa.

**Causa común.** Asignar texto a un número, un número decimal a un `int` sin redondear, o un `bool` donde se espera otra cosa.

**Ejemplo que lo genera.**

```
int edad = 20
edad = "veinte"   // NX07: no se puede asignar string a una variable int
```

**Solución paso a paso.**

1. Revisa el tipo declarado de la variable.
2. Revisa el tipo del valor que le asignas.
3. Convierte el valor al tipo esperado con una conversión válida, o cambia el tipo de la variable si diseño era incorrecto.

```
int edad = 20
edad = 21                    // ok: entero a entero

string entrada = "20"
int edad2 = int(entrada)     // ok: conversión explícita de string a int
```

**Cómo evitarlo.** Respeta un solo tipo por variable. Al leer con `Console.input`, declara la variable con el tipo esperado (`int edad = Console.input(...)`) para que la conversión la haga la entrada, no tú. No mezcles tipos; si necesitas cambiar de tipo, usa una conversión explícita documentada.

---

# Categoría: Tipos y evaluación (NX10–NX19)

## NX10: Operandos con tipos incompatibles

**Descripción.** Se usó un **operador con operandos de tipos que no se pueden combinar**. Por ejemplo, sumar un `string` con un `int`, o restar un `bool` de un número. Nexis no convierte tipos automáticamente en operaciones mixtas.

**Causa común.** Sumar texto y número para "concatenar", o intentar operar un valor que `Console.input` devolvió como `string`.

**Ejemplo que lo genera.**

```
int resultado = "5" + 5    // NX10: no se puede sumar string + int
bool r2 = true + 1         // NX10: no se puede sumar bool + int
```

**Solución paso a paso.**

1. Identifica el tipo de cada operando (puedes usar `auto` y pistas del contexto, o revisar la declaración).
2. Si uno de ellos vino de `Console.input` sin tipo, recuérdalo: por defecto es `string`.
3. Convierte explícitamente el operando al tipo correcto.

```
string s = "5"
int cinco = int(s)
int resultado = cinco + 5      // 10

int n = 4
bool valido = true
int suma = n + 1               // ok, solo ints
// true + 1 no tiene sentido lógico; usa condicionales en su lugar
```

**Cómo evitarlo.** Declara el tipo esperado al leer entradas (`int n = Console.input(...)`), verifica tipos antes de operar y no intentes "sumar" textos con números. Para concatenar texto, usa `+` solo entre `string`.

---

## NX11: Índice fuera de rango

**Descripción.** Se accedió a una **posición inexistente** de un vector u otra colección indexada: el índice es negativo o mayor/igual que `longitud()`. Se corresponde con la excepción `ErrorIndice`.

**Causa común.** Pedir un índice por teclado sin validarlo, usar índices que arrancan en `1` (cuando Nexis usa base 0) o recorrer con un límite incorrecto.

**Ejemplo que lo genera.**

```
Vector<int> nums = [10, 20, 30]
int valor = nums.obtener(5)   // NX11: índice 5 fuera de rango (longitud = 3)
```

**Solución paso a paso.**

1. Confirma la longitud de la colección: `nums.longitud()`.
2. Comprueba que el índice cumpla `0 <= indice < longitud`.
3. Valida antes de acceder o captura el error:

```
int indice = Console.input(text="Posición: ")
if (indice >= 0 && indice < nums.longitud()) {
    Console.print(nums.obtener(indice))
} else {
    Console.print("Posición inválida")
}
```

4. Si el índice puede fallar por lógica ajena, usa `try/catch` con `ErrorIndice`.

**Cómo evitarlo.** Recuerda que los índices empiezan en `0`, siempre compara contra `longitud() - 1` para el último elemento y valida cualquier índice que venga del usuario.

---

## NX12: Conversión de tipo inválida

**Descripción.** Se intentó **convertir un valor a un tipo con el que no es compatible**, normalmente pasando texto que no tiene el formato esperado a un número. Se corresponde con `ErrorTipo` o `ErrorValidacion` según el contexto.

**Causa común.** Convertir un texto como `"abc"` a entero, o un texto con formato de otro país/idioma (por ejemplo `"3,5"` en lugar de `"3.5"`).

**Ejemplo que lo genera.**

```
int edad = int("abc")   // NX12: impossible convertir 'abc' a entero
```

**Solución paso a paso.**

1. Valida el texto antes de convertir:

```
string entrada = Console.input(text="Edad: ")
if (string.es_numero(entrada)) {   // o usa expresiones regulares si están disponibles
    int edad = int(entrada)
} else {
    Console.print("Ingrese un número válido")
}
```

2. Captura el error con `try/catch`:

```
try {
    int edad = int(entrada)
} catch (ErrorValidacion e) {
    Console.print("El valor ingresado no es un número")
}
```

3. Verifica el formato del texto (punto decimal, sin espacios ni símbolos).

**Cómo evitarlo.** Cuando un valor entra por teclado, declara su tipo directamente (`int edad = Console.input(...)`) para que la validación ocurra al leer. No conviertas valores sin revisar antes su contenido.

---

## NX13: Operación matemática inválida

**Descripción.** Se ejecutó una **operación matemática fuera del dominio permitido**: por ejemplo, raíz cuadrada de un número negativo o logaritmo de un valor no positivo usando el dominio real. Se corresponde con `ErrorMatematico`/`ErrorDivision`.

**Causa común.** Calcular `sqrt` de un número negativo por datos de entrada no validados.

**Ejemplo que lo genera.**

```
#inject math;

float resultado = math.sqrt(-9)   // NX13: raíz de número negativo (reales)
```

**Solución paso a paso.**

1. Valida el argumento antes de llamar:

```
float valor = Console.input(text="Número: ")
if (valor >= 0) {
    float resultado = math.sqrt(valor)
} else {
    Console.print("Ingrese un valor no negativo")
}
```

2. O captura la excepción:

```
try {
    float resultado = math.sqrt(valor)
} catch (ErrorMatematico e) {
    Console.print("La operación no está definida para ese valor")
}
```

**Cómo evitarlo.** Conoce el dominio de cada función matemática: `sqrt` y `log` exigen valores positivos; las funciones trigonométricas reciben radianes. Valida siempre cuando el dato provenga del usuario.

---

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

**Causa común.** Copiar la definición de una función, o importar dos módulos que exponen una función con el mismo nombre (ver [NX82](#nx82-función-usada-sin-importar)).

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

**Cómo evitarlo.** Usa nombres descriptivos y únicos para cada función. Si dos módulos importados definen la misma función, usa alias o renombra al importar (ver [NX82](#nx82-función-usada-sin-importar)).

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
    int valor = nums.obtener(9)
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
Console.print(nums.obtener(8))   // NX42: error no capturado (ErrorIndice)
```

**Solución paso a paso.**

1. Lee el reporte: te indica el tipo de error y dónde ocurrió.
2. Envuelve la operación riesgosa en `try/catch`:

```
try {
    Vector<int> nums = [1, 2, 3]
    Console.print(nums.obtener(8))
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

**Cómo evitarlo.** `lanzar` siempre recibe `ErrorTipo("mensaje")`, nunca literales directos. Revisa la tabla de tipos de error en [try_catch.md](language/errors/try_catch.md).

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

# Categoría: Colecciones (NX50–NX59)

## NX50: Operación sobre colección vacía

**Descripción.** Se intentó **extraer, leer o inspeccionar el primer/último elemento de una colección vacía**: `extraer()`, `desapilar()`, `desencolar()`, `cima()`, `frente()`, `primero()`, `ultimo()`.

**Causa común.** Olvidar verificar con `esta_vacia()`/`esta_vacio()` antes de consumir un elemento.

**Ejemplo que lo genera.**

```
Stack<int> pila = Stack()
int valor = pila.desapilar()   // NX50: la pila está vacía
```

**Solución paso a paso.**

1. Verifica el estado antes de operar.

```
if (!pila.esta_vacia()) {
    int valor = pila.desapilar()
} else {
    Console.print("No hay elementos")
}
```

2. O captura la excepción con `try/catch`.

**Cómo evitarlo.** Antes de cada `desapilar`, `desencolar`, `extraer`, `frente`, `cima`, `primero` o `ultimo`, pregunta siempre si hay elementos. En bucles de consumo, la condición del bucle suele ser `while (!estructura.esta_vacia())`.

---

## NX51: Modificar colección durante iteración

**Descripción.** Se intentó **agregar o eliminar elementos de una colección mientras se recorre** con `foreach` (o con un `for` basado en índices que cambia el tamaño). El comportamiento es indeterminado, por lo que Nexis lo rechaza.

**Causa común.** Eliminar elementos de un vector dentro de un `foreach` para "filtrarlos".

**Ejemplo que lo genera.**

```
foreach (numero in numeros) {
    if (numero < 0) {
        numeros.eliminar(indice)   // NX51: modificar durante la iteración
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
        filtrados.agregar(numero)
    }
}
```

**Cómo evitarlo.** Nunca agregues ni elimines en la misma colección que estás recorriendo. Crea colecciones nuevas cuando necesites filtrar o transformar.

---

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

string contenido = file.leer("datos_inexistentes.txt")   // NX61
```

**Solución paso a paso.**

1. Comprueba la ruta exacta.
2. Verifica la existencia antes de operar:

```
if (file.existe("datos.txt")) {
    string contenido = file.leer("datos.txt")
} else {
    Console.print("El archivo no existe")
}
```

3. O captura el error con `try/catch` (`ErrorArchivo`).

**Cómo evitarlo.** Usa `file.existe(ruta)` antes de leer o eliminar. Para datos de prueba, garantiza que el archivo se cree (con `file.escribir`) antes de intentar leerlo.

---

## NX62: Error de lectura/escritura

**Descripción.** Una operación de `file` **no pudo completarse por una razón distinta a "no existe"**: permisos insuficientes, el archivo está bloqueado, el disco está lleno o la ruta es inválida. Se corresponde con `ErrorArchivo`.

**Causa común.** Escribir en un directorio sin permisos o intentar sobreescribir mientras el archivo está en uso.

**Ejemplo que lo genera.**

```
file.escribir("/root/datos_protegidos.txt", "contenido")   // NX62 sin permisos
```

**Solución paso a paso.**

1. Revisa los permisos de la ruta y el tipo de operación.
2. Asegúrate de que el directorio exista (`file.crear_directorio`) antes de escribir.
3. Captura el error para no abortar el programa:

```
try {
    file.escribir("salida.txt", contenido)
} catch (ErrorArchivo e) {
    Console.print("No se pudo guardar el archivo: " + e.mensaje())
}
```

**Cómo evitarlo.** Escribe siempre en rutas con permisos de escritura conocidos y crea los directorios antes de usarlos. Captura `ErrorArchivo` cuando la operación pueda fallar por el entorno.

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

## Buenas prácticas generales

1. **Lee el código en el mensaje de error:** identifica la línea exacta antes de buscar la solución.
2. **Agrupa errores por categoría:** los códigos `NX00–NX09` son de variables, `NX10–NX19` de tipos, `NX20–NX29` de control de flujo, `NX30–NX39` de funciones, `NX40–NX49` de manejo de errores, `NX50–NX59` de colecciones, `NX60–NX69` de E/S y archivos, `NX70–NX79` de red/gráficos, `NX80–NX89` de módulos y `NX90–NX99` de sintaxis y sistema.
3. **Documenta qué errores puede lanzar cada función tuya:** ayuda a quien consuma tu código y a ti mismo.
4. **Se específico en los mensajes:** al lanzar `ErrorValidacion("...")`, describe exactamente el problema.