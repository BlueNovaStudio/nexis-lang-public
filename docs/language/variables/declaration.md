# 📘 Declaración e Inicialización en Nexis

## 1. Declaración de variables

La declaración define una variable y su tipo, pero **sin asignarle un valor inicial**.

### Sintaxis:

```
tipo_dato nombre_variable;
```

> **Regla:**  
> El tipo de dato va **antes** del nombre de la variable.  
> **Lleva punto y coma (`;`)** al final.

### Ejemplos:

```
int n;              // entero
string nombre;      // cadena de texto
char letra;         // carácter
float precio;       // decimal (precisión simple)
double salario;     // decimal (precisión doble)
bool valor;         // verdadero/falso
const double PI;    // constante (requiere inicialización)
```

---

## 2. Inicialización de variables

Inicializar es **asignar un valor por primera vez** a una variable.

### Sintaxis:

```
nombre_variable = valor
```

> **Regla:**  
> La inicialización **No lleva punto y coma (`;`)**.

### Ejemplos:

```
n = 16
nombre = "Ana"
letra = 'Z'
precio = 99.99f
salario = 1500.50
valor = true
PI = 3.14159
```

---

## 3. Declaración e inicialización en una sola línea

Nexis permite **declarar e inicializar** al mismo tiempo.

### Sintaxis:

```
tipo nombre_variable = valor
```

### Ejemplos:

```
int edad = 25
string ciudad = "Lima"
float temperatura = 23.5f
bool activo = false
const double GRAVEDAD = 9.81
```

---

## 4. Declarar primero, inicializar después

También es válido **declarar una variable y luego inicializarla más adelante** en el código.

### Ejemplo:

```
int contador;         // declaración
contador = 10         // inicialización posterior
```

Esto es útil cuando el valor inicial no se conoce en el momento de la declaración.

---

## 5. El operador `auto`

Nexis incluye el operador `auto`, que permite **deducir automáticamente el tipo** a partir del valor asignado.

### Sintaxis:

```
auto nombre_variable = valor
```

### Ejemplos:

```
auto n = 16             // auto deduce int
auto nombre = "Carlos"  // auto deduce string
auto altura = 1.75      // auto deduce double
auto activo = true      // auto deduce bool
```

> 💡 `auto` solo funciona si **inicializas en la misma línea**.

---

## 6. Constantes (`const`)

Las constantes se declaran con `const` y **deben inicializarse obligatoriamente** en el momento de la declaración.

### Correcto:

```
const double PI = 3.14159
```

### Incorrecto (error):

```
const double PI;   // falta inicialización
PI = 3.14159       // error: no se puede asignar después
```

---

## 7. Reglas generales de sintaxis

| Acción | Sintaxis | ¿Lleva `;`? |
|--------|----------|-------------|
| Declarar | `tipo nombre` | Si |
| Inicializar | `nombre = valor` | No |
| Declarar + Inicializar | `tipo nombre = valor` | No |
| Declarar con `auto` | `auto nombre = valor` | No |
| Declarar constante | `const tipo nombre = valor` | No |

---

## 8. Error común

En Nexis, **declarar una variable sin inicializarla no genera error**, pero usarla antes de inicializarla **sí lo genera**.

### Incorrecto:

```
int x
Console.print(x)   // error: x no ha sido inicializada
```

### Correcto:

```
int x
x = 5
Console.print(x)   // imprime 5
```