# 📘 Impresión y Lectura en Nexis

## Introducción

La entrada y salida son esenciales en cualquier lenguaje de programación. Permiten comunicar al usuario con el programa mediante mensajes, resultados y datos capturados.

## Navegación

- [Volver a variables](README.md)
- [Declaración e inicialización](declaration.md)
- [Operadores](../operadores/operadores.md)

---

## 1. Salida de datos (Console.print)

Se usa para mostrar información en pantalla.

### Sintaxis general

```
Console.print(valor)
Console.print(valor1, valor2, ...)   // variante con varios argumentos
```

### Ejemplos

```
Console.print("Hola, mundo")

int edad = 20
Console.print(edad)

string nombre = "Ana"
Console.print("Mi nombre es " + nombre)

// Con varios argumentos: se separan con comas
Console.print("El area del circulo es: ", area)
Console.print("Nombre:", nombre, "- Edad:", edad)
```

### `Console.println`

`Console.println` funciona igual que `Console.print` pero **añade un salto de línea** al final. Úsalo para separar resultados:

```
Console.println("Primera línea")
Console.println("Segunda línea")
```

### Interpolación con `fs"..."`

Puedes insertar valores dentro de un texto usando `fs` seguido de comillas dobles y `{variable}`:

```
int a = 3
int b = 2
Console.print(fs"Valores -> a: {a} | b: {b}")   // Valores -> a: 3 | b: 2
```

El prefijo `fs` (formato de string) evalúa cada `{...}` dentro del texto.

### Consejos

- Usa mensajes claros y descriptivos.
- Combina texto con variables cuando necesites mostrar resultados.
- No abuses de líneas largas; haz la salida legible.

---

## 2. Entrada de datos (Console.input)

Se usa para capturar información proporcionada por el usuario.

### Sintaxis general

```
auto variable = Console.input(text="Mensaje a mostrar")
```

### Reglas importantes

- El tipo de dato se define al declarar la variable.
- Si no se especifica el tipo, `auto` tomará el valor ingresado como `string`.
- El mensaje en `text` es opcional, pero recomendado para guiar al usuario.

---

### Ejemplo 1: Entrada como string (por defecto)

```
auto nombre = Console.input(text="Ingrese su nombre: ")
Console.print("Hola, " + nombre)
```

En este caso, `nombre` será de tipo `string`.

---

### Ejemplo 2: Entrada con tipo específico

Se puede declarar la variable con el tipo deseado:

```
int edad = Console.input(text="Ingrese su edad: ")
Console.print("Tu edad es: " + edad)
```

También se puede usar `auto` y el tipo se deducirá automáticamente:

```
auto edad = Console.input(text="Ingrese su edad: ")
```

> **Nota:** Aunque `auto` deduce el tipo, es preferible especificar el tipo de dato que se espera recibir para evitar errores y hacer el código más claro.

---

### Ejemplo 3: Entrada de números decimales

```
float altura = Console.input(text="Ingrese su altura: ")
Console.print("Su altura es: " + altura)
```

Para valores decimales, se recomienda usar `float` para precisión simple o `double` para precisión doble.

---

### Ejemplo 4: Entrada de valores booleanos

```
bool activo = Console.input(text="¿Está activo? (true/false): ")
Console.print("Estado: " + activo)
```

El usuario debe ingresar `true` o `false`.

---

## 3. Combinación de salida y entrada

Un programa típico sigue este patrón:

```
auto nombre = Console.input(text="Ingrese su nombre: ")
Console.print("Bienvenido, " + nombre)

int edad = Console.input(text="Ingrese su edad: ")
Console.print("Tienes " + edad + " años")
```

---

## 4. Resumen de tipos en Console.input

| Declaración | Tipo resultante |
|-------------|-----------------|
| `auto variable = Console.input(...)` | `string` (por defecto) |
| `string variable = Console.input(...)` | `string` |
| `int variable = Console.input(...)` | `int` |
| `float variable = Console.input(...)` | `float` |
| `double variable = Console.input(...)` | `double` |
| `bool variable = Console.input(...)` | `bool` |

---

## 5. Errores comunes

### Error 1: No especificar el tipo esperado

```
auto edad = Console.input(text="Ingrese su edad: ")
// edad es string, no se puede operar como número
int suma = edad + 5   // error: tipos incompatibles
```

**Solución:** Especificar el tipo al declarar.

```
int edad = Console.input(text="Ingrese su edad: ")
```

### Error 2: Ingresar un valor incorrecto

```
int edad = Console.input(text="Ingrese su edad: ")
// Si el usuario ingresa "veinte" en lugar de "20", ocurrirá un error
```

**Solución:** Validar la entrada o usar manejo de errores.

---

## 6. Buenas prácticas

1. **Usa mensajes claros:** Indica exactamente qué se espera del usuario.

```
Console.input(text="Ingrese su nombre (solo letras): ")
```

2. **Especifica el tipo:** Evita usar `auto` en entradas si esperas un tipo específico.

```
float precio = Console.input(text="Ingrese el precio: ")
```

3. **Valida la entrada:** Siempre verifica que los datos ingresados sean válidos antes de usarlos.

4. **Muestra resultados inmediatos:** Usa `Console.print` para confirmar la entrada del usuario.

```
int edad = Console.input(text="Ingrese su edad: ")
Console.print("Edad registrada: " + edad)
```
