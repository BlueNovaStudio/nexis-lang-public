# 📘 Operadores en Nexis

Los operadores permiten realizar cálculos, comparaciones y decisiones dentro de un programa. En Nexis están organizados por categorías para que el uso de cada uno sea más claro.

## Navegación

- [Documentación principal](../README.md)
- [Variables y entrada/salida](../variables/README.md)
- [Catálogo de errores NX](../errors/errors.md)

---

## 1. Operadores aritméticos

Se usan para realizar cálculos matemáticos básicos.

| Operador | Nombre | Ejemplo |
|----------|--------|---------|
| `+` | Suma | `a + b` |
| `-` | Resta | `a - b` |
| `*` | Multiplicación | `a * b` |
| `/` | División | `a / b` |
| `%` | Módulo | `a % b` |
| `**` | Potencia | `a ** b` |
| `++` | Incremento | `a++` |
| `--` | Decremento | `a--` |

### Ejemplo

```nexis
int a = 10
int b = 3

int suma = a + b             // 13
int resta = a - b            // 7
int multiplicacion = a * b   // 30
int division = a / b         // 3
int modulo = a % b           // 1
int potencia = a ** b        // 1000

a++
b--
```

> La división entre enteros puede devolver un valor entero. Si quieres un decimal, usa `float` o `double`.

---

## 2. Operadores de asignación

Se usan para guardar valores dentro de una variable.

| Operador | Ejemplo | Equivalente |
|----------|---------|-------------|
| `=` | `a = 5` | `a = 5` |
| `+=` | `a += 3` | `a = a + 3` |
| `-=` | `a -= 3` | `a = a - 3` |
| `*=` | `a *= 3` | `a = a * 3` |
| `/=` | `a /= 3` | `a = a / 3` |
| `%=` | `a %= 3` | `a = a % 3` |
| `**=` | `a **= 3` | `a = a ** 3` |

### Ejemplo

```nexis
int x = 10
x += 5
x -= 3
x *= 2
x /= 4
x %= 4
x **= 3
```

---

## 3. Operadores de comparación

Devuelven un valor booleano: `true` o `false`.

| Operador | Nombre | Ejemplo |
|----------|--------|---------|
| `==` | Igual a | `a == b` |
| `!=` | Diferente de | `a != b` |
| `>` | Mayor que | `a > b` |
| `<` | Menor que | `a < b` |
| `>=` | Mayor o igual | `a >= b` |
| `<=` | Menor o igual | `a <= b` |

### Ejemplo

```nexis
int a = 10
int b = 5

bool igual = a == b
bool diferente = a != b
bool mayor = a > b
bool menor = a < b
```

---

## 4. Operadores lógicos

Permiten combinar condiciones.

| Operador | Nombre | Descripción |
|----------|--------|-------------|
| `&&` | AND | Verdadero si ambas condiciones son verdaderas |
| `||` | OR | Verdadero si al menos una es verdadera |
| `!` | NOT | Invierte el valor booleano |

### Ejemplo

```nexis
bool mayorDeEdad = edad >= 18
bool tienePermiso = true

bool puedeEntrar = mayorDeEdad && tienePermiso
bool puedePasar = mayorDeEdad || tienePermiso
bool esMenor = !mayorDeEdad
```

---

## 5. Operador ternario

Nexis también incluye una forma visual y segura de representar una decisión binaria con evaluación perezosa.

### Sintaxis

```plaintext
variable_destino = (condicion_logica) => [expresion_si_verdadera] <--> [expresion_si_falsa]
```

### Descripción

| Operador | Nombre | Función |
|----------|--------|---------|
| `=>` | Implicación / resolución | Selecciona la rama según el resultado de la condición |
| `<-->` | Bifurcación exclusiva | Marca la separación entre la opción verdadera y la falsa |

### Comportamiento

- Primero se evalúa solo la condición.
- Si es verdadera, ejecuta solo la rama izquierda.
- Si es falsa, ejecuta solo la rama derecha.
- La rama no seleccionada no se evalúa ni ejecuta.

### Ejemplos

```nexis
int edad = 20
string estado = (edad >= 18) => "Mayor de edad" <--> "Menor de edad"
```

```nexis
divisor = 0
resultado = (divisor != 0) => (100 / divisor) <--> 0
```

```nexis
saldo_disponible = 500
costo_compra = 800

(saldo_disponible >= costo_compra) => ProcesarPago() <--> RechazarTransaccion()
```

> Esta sintaxis es útil para decisiones compactas, prevención de errores y reducción de evaluaciones innecesarias.

---

## 6. Precedencia de operadores

Cuando hay varias operaciones en una línea, se resuelven siguiendo este orden:

1. Paréntesis `()`
2. Potencia `**`
3. Multiplicación, división y módulo `* / %`
4. Suma y resta `+ -`
5. Comparaciones `> < >= <=`
6. Igualdad `== !=`
7. AND `&&`
8. OR `||`
9. Asignación `= += -= *= /= %=`
10. Decisión estructural `=> <-->`

### Ejemplo

```nexis
int resultado = 5 + 3 * 2 ** 2
// 2 ** 2 = 4
// 3 * 4 = 12
// 5 + 12 = 17
```

---

## 7. Errores comunes

### División entre cero

```nexis
int valor = 10 / 0
```

### Operandos incompatibles

```nexis
string texto = "Hola"
int resultado = texto + 5
```

---

## 8. Resumen

Los operadores te permiten:

- calcular valores,
- comparar datos,
- tomar decisiones,
- modificar variables de forma compacta,
- representar bifurcaciones condicionales con una lógica segura y eficiente.

Aprender su uso correcto hace que el código sea más claro y menos propenso a errores.