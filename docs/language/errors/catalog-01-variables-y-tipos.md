# Catálogo de errores: Variables, constantes y tipos (NX00–NX19)

Parte del [catálogo de errores de Nexis](errors.md). Cada código
incluye descripción, causa, ejemplo, solución paso a paso y cómo
evitarlo.

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

4. También puedes capturarlo con `try/catch` y `ErrorDivision` (ver [NX42](catalog-03-errores-y-colecciones.md#nx42-error-no-capturado)).

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

## NX08: Variable `auto` sin inicializador

**Descripción.** Se declaró una variable con `auto` **sin asignarle un valor en la misma línea**. Con `auto` el tipo se deduce del valor inicial: sin ese valor no hay tipo ni valor posible.

**Causa común.** Escribir `auto contador;` para asignar después, imitando la declaración con tipo explícito.

**Ejemplo que lo genera.**

```
auto contador;   // NX08: auto exige inicialización en la misma línea
```

**Solución paso a paso.**

1. Inicializa en la misma declaración:

```
auto contador = 0
```

2. Si el valor se conoce más adelante, usa un tipo explícito:

```
int contador;
// ... más tarde
contador = 0
```

**Cómo evitarlo.** Usa `auto` únicamente cuando puedas escribir el valor en la misma línea. Si vas a asignar después, declara con tipo explícito.

---

## NX09: Valor fuera del rango del tipo

**Descripción.** Un literal o el valor asignado **no cabe en el tipo declarado**: supera el máximo o es inferior al mínimo. Cada tipo de Nexis tiene un rango (`int` de 32 bits, `long` de 64 bits, etc.).

**Causa común.** `int x = 4000000000` (excede el máximo de `int`) o una suma cuyo resultado desborda.

**Ejemplo que lo genera.**

```
int x = 4000000000   // NX09: 4000000000 no cabe en un int (32 bits)
```

**Solución paso a paso.**

1. Elige un tipo con rango suficiente:

```
long x = 4000000000L
```

2. Revisa los literales que intervienen y usa sufijos (`L`, `LL`, `u`, `uL`, `f`) cuando corresponda.
3. Si el desbordamiento ocurre al ejecutar operaciones, captúralo con `try/catch` (`ErrorMatematico`) — ver [NX19](#nx19-desbordamiento-aritmético-en-ejecución).

**Cómo evitarlo.** Conoce el rango del tipo antes de asignar. Para contadores o totales grandes usa `long`; para valores sin signo usa `unsigned int`/`unsigned long`.

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
int valor = nums.get(5)   // NX11: índice 5 fuera de rango (longitud = 3)
```

**Solución paso a paso.**

1. Confirma la longitud de la colección: `nums.length()`.
2. Comprueba que el índice cumpla `0 <= indice < longitud`.
3. Valida antes de acceder o captura el error:

```
int indice = Console.input(text="Posición: ")
if (indice >= 0 && indice < nums.length()) {
    Console.print(nums.get(indice))
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

## NX14: Tipo de retorno incompatible

**Descripción.** El valor de un `emit -> valor` **no coincide con el tipo declarado** tras `->`. Por ejemplo, una función `-> int` que emite un `string`.

**Causa común.** Cambiar el tipo de retorno de la función y olvidar actualizar sus `emit`.

**Ejemplo que lo genera.**

```
func obtener_etiqueta() -> int {
    emit -> "etiqueta"   // NX14: el tipo del emit (string) no coincide con int
}
```

**Solución paso a paso.**

1. Convierte el valor al tipo declarado:

```
func obtener_etiqueta() -> int {
    emit -> int("42")
}
```

2. O declara el tipo de retorno correcto:

```
func obtener_etiqueta() -> string {
    emit -> "etiqueta"
}
```

**Cómo evitarlo.** Mantén el tipo del `emit` igual al declarado. Para conversiones usa las funciones de conversión documentadas ([NX12](#nx12-conversión-de-tipo-inválida)).

---

## NX15: Tipo no reconocido

**Descripción.** Se usó un **tipo que no existe en Nexis**: está mal escrito o no pertenece al conjunto de tipos del lenguaje.

**Causa común.** `intger x`, `Vectorr<int>` o inventar un tipo propio en lugar de usar `struct`/`class`.

**Ejemplo que lo genera.**

```
Zapato<int> z = Zapato()   // NX15: el tipo 'Zapato' no existe
```

**Solución paso a paso.**

1. Verifica la ortografía. Tipos básicos: `int`, `long`, `long long`, `short`, `unsigned int`, `unsigned long`, `float`, `double`, `long double`, `char`, `string`, `bool`.
2. Para colecciones usa `Vector<T>`, `Stack<T>`, `Queue<T>`, `Set<T>`, `Map<K, V>`, `LinkedList<T>`, `Tree<T>`, `Graph<T>`, `Trie`.
3. Si necesitas un tipo propio (agrupación de datos), define un `struct` o `class` y usa su nombre.

**Cómo evitarlo.** Revisa el catálogo de tipos antes de escribir el nombre. Los tipos propios se declaran con `struct`/`class` antes de usarse.

---

## NX16: Carácter inválido

**Descripción.** Un literal `char` **no contiene exactamente un carácter**: tiene más de uno o está vacío. Nexis solo admite un carácter entre comillas simples.

**Causa común.** Escribir `'abc'` por error, o `''` pensando que significa "sin valor".

**Ejemplo que lo genera.**

```
char letra = 'abc'   // NX16: un char admite un único carácter
```

**Solución paso a paso.**

1. Escribe un único carácter:

```
char letra = 'a'
```

2. Si necesitas una secuencia de caracteres, usa `string`:

```
string letras = "abc"
```

**Cómo evitarlo.** Comillas simples `'...'` = un carácter; comillas dobles `"..."` = texto.

---

## NX17: Índice o clave de tipo inválido

**Descripción.** Se accedió a una colección con una **clave o índice del tipo equivocado**: un `string` como índice de un `Vector`, o una clave de tipo distinto al que declara un `Map<K, V>`.

**Causa común.** `nums.get("primero")` en un `Vector<int>`, o `inventario.get(1)` cuando el mapa es `Map<string, int>`.

**Ejemplo que lo genera.**

```
Vector<int> numeros = [1, 2, 3]
int x = numeros.get("dos")   // NX17: el índice de un Vector debe ser un entero
```

**Solución paso a paso.**

1. Revisa el tipo parametrizado de la colección (`Vector<int>` → índices `int`, `Map<string, int>` → claves `string`).
2. Usa el tipo correcto:

```
int x = numeros.get(1)
```

**Cómo evitarlo.** El índice de colecciones indexadas siempre es `int`; las claves de un `Map` deben coincidir con el tipo `K` declarado.

---

## NX18: Comparación entre tipos incompatibles

**Descripción.** Se aplicó un **operador de orden** (`<`, `<=`, `>`, `>=`) a valores que no se pueden ordenar entre sí: un `bool`, o un `string` con un número. `==` y `!=` comparan igualdad; el orden exige tipos con una relación de orden definida.

**Causa común.** `if (true < false)`, o comparar una edad `int` con un texto.

**Ejemplo que lo genera.**

```
if (true < false) {   // NX18: bool no tiene un orden definido
    Console.print("¿?")
}
```

**Solución paso a paso.**

1. Compara valores del mismo tipo ordenable (números).
2. Convierte antes de comparar o cambia el diseño:

```
if (edad >= 18) { ... }   // números con números
```

**Cómo evitarlo.** Usa `<`, `<=`, `>`, `>=` solo entre números; `==`/`!=` sirven para el resto.

---

## NX19: Desbordamiento aritmético en ejecución

**Descripción.** El **resultado de una operación en tiempo de ejecución supera el rango** del tipo resultante, aunque los operandos individuales sean válidos. Es distinto de [NX09](#nx09-valor-fuera-del-rango-del-tipo), que se detecta en literales y asignaciones estáticas.

**Causa común.** `int a = 2000000000; Console.print(a + a)`.

**Ejemplo que lo genera.**

```
int a = 2000000000
int b = 2000000000
Console.print(a + b)   // NX19: el resultado desborda el rango de int
```

**Solución paso a paso.**

1. Elige un tipo con rango suficiente para el resultado (`long a = 2000000000L`).
2. Valida los valores antes de operar cuando vengan de datos externos.
3. Captura el error en ejecución con `try/catch` (`ErrorMatematico`).

**Cómo evitarlo.** Dimensiona los tipos según el peor resultado posible de tus operaciones y revisa las sumas y productos acumulativos.

---

---

- Siguiente: [Control de flujo y funciones (NX20–NX39)](catalog-02-control-y-funciones.md)
- [Volver al índice de errores](errors.md)
