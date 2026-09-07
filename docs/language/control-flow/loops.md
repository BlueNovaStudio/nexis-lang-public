Entendido. Aquí tienes la versión revisada de **Bucles en Nexis** con una **nueva sintaxis para `for`**, diseñada para ser más clara, legible y diferente a la de C++.

---

# 📘 Bucles en Nexis

## Introducción

Los bucles permiten ejecutar un bloque de código repetidamente mientras se cumpla una condición. Nexis ofrece **cuatro tipos de bucles** para adaptarse a diferentes necesidades: `while`, `do while`, `for` y `foreach`.

---

## 1. Bucle `while`

El bucle `while` ejecuta un bloque de código **mientras** la condición sea verdadera. La condición se evalúa **antes** de cada iteración.

### Sintaxis

```
while (condicion) {
    // código a repetir
}
```

### Características

- La condición se evalúa al inicio de cada iteración.
- Si la condición es falsa desde el principio, el bloque no se ejecuta.
- Puede ejecutarse indefinidamente (bucle infinito) si la condición siempre es verdadera.

### Ejemplo 1: Contador básico

```
int contador = 0

while (contador < 5) {
    Console.print(contador)
    contador = contador + 1
}
// Salida: 0, 1, 2, 3, 4
```

### Ejemplo 2: Con entrada de usuario

```
bool continuar = true

while (continuar) {
    auto opcion = Console.input(text="¿Desea continuar? (s/n): ")
    
    if (opcion == "n"):
        continuar = false
    else:
        Console.print("Continuando...")
}
```

### Ejemplo 3: Bucle infinito (con `break`)

```
int intentos = 0

while (true) {
    intentos = intentos + 1
    Console.print("Intento " + intentos)
    
    if (intentos >= 3):
        break   // sale del bucle
}
// Salida: Intento 1, Intento 2, Intento 3
```

---

## 2. Bucle `do while`

El bucle `do while` ejecuta el bloque de código **primero** y luego evalúa la condición. Esto garantiza que el bloque se ejecute **al menos una vez**.

### Sintaxis

```
do {
    // código a repetir
} while (condicion)
```

### Características

- El bloque se ejecuta **al menos una vez**, incluso si la condición es falsa.
- La condición se evalúa después de cada iteración.
- Útil cuando necesitas que el código se ejecute antes de verificar la condición.

### Ejemplo 1: Menú interactivo

```
int opcion

do {
    Console.print("--- Menú Principal ---")
    Console.print("1. Saludar")
    Console.print("2. Despedirse")
    Console.print("3. Salir")
    
    opcion = Console.input(text="Seleccione una opción: ")
    
    if (opcion == 1):
        Console.print("¡Hola!")
    else if (opcion == 2):
        Console.print("¡Adiós!")
    else if (opcion == 3):
        Console.print("Saliendo del programa...")
    else:
        Console.print("Opción inválida")
} while (opcion != 3)
```

### Ejemplo 2: Validación de entrada

```
int edad

do {
    edad = Console.input(text="Ingrese su edad (mayor a 0): ")
} while (edad <= 0)

Console.print("Edad válida: " + edad)
```

---

## 3. Bucle `for`

En Nexis, el bucle `for` tiene una sintaxis más natural y legible.

### Sintaxis

```
for variable in rango {
    // código a repetir
}
```

### Características

- `variable` toma cada valor del rango especificado.
- El rango se define con el operador `..` (inclusive).
- No necesita inicialización, condición ni actualización explícitas.
- Es más legible y menos propenso a errores.

### Ejemplo 1: Rango básico

```
for i in 0 .. 5 {
    Console.print(i)
}
// Salida: 0, 1, 2, 3, 4, 5
```

### Ejemplo 2: Con paso personalizado (usando `step`)

```
for i in 0 .. 10 step 2 {
    Console.print(i)
}
// Salida: 0, 2, 4, 6, 8, 10
```

### Ejemplo 3: Rango descendente

```
for i in 5 .. 0 {
    Console.print(i)
}
// Salida: 5, 4, 3, 2, 1, 0
```

### Ejemplo 4: Sin límite superior (hasta que se cumpla condición)

```
for i in 0 .. while (i < 10) {
    Console.print(i)
    i = i + 1
}
// Salida: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
```

### Ejemplo 5: Con `break`

```
for i in 0 .. 10 {
    if (i == 5):
        break
    
    Console.print(i)
}
// Salida: 0, 1, 2, 3, 4
```

### Ejemplo 6: Con `continue`

```
for i in 0 .. 5 {
    if (i == 2):
        continue
    
    Console.print(i)
}
// Salida: 0, 1, 3, 4, 5
```

---

## 4. Bucle `foreach`

El bucle `foreach` se utiliza para iterar sobre **colecciones** como arreglos, listas o conjuntos. Es similar a `for` pero específico para colecciones.

### Sintaxis

```
foreach (variable in coleccion) {
    // código a repetir
}
```

### Características

- Itera automáticamente sobre cada elemento de la colección.
- No necesita índice ni control de límites.
- Es más seguro y legible para recorrer colecciones.
- El tipo de la variable puede ser `auto` para deducción automática.

### Ejemplo 1: Recorrer un vector

```
#inject vector;

Vector<int> numeros = [10, 20, 30, 40, 50]

foreach (numero in numeros) {
    Console.print(numero)
}
// Salida: 10, 20, 30, 40, 50
```

### Ejemplo 2: Con tipo específico

```
#inject vector;

Vector<string> nombres = ["Ana", "Luis", "Carlos", "María"]

foreach (string nombre in nombres) {
    Console.print("Hola, " + nombre)
}
// Salida: Hola, Ana; Hola, Luis; Hola, Carlos; Hola, María
```

### Ejemplo 3: Con auto (deducción de tipo)

```
#inject vector;

Vector<int> edades = [18, 25, 30, 22, 27]

foreach (auto edad in edades) {
    if (edad >= 18):
        Console.print("Mayor de edad: " + edad)
}
```

### Ejemplo 4: Con condición dentro del bucle

```
#inject vector;

Vector<float> precios = [10.5f, 25.0f, 15.75f, 30.0f]

foreach (precio in precios) {
    if (precio > 20.0f):
        Console.print("Precio alto: " + precio)
    else:
        Console.print("Precio bajo: " + precio)
}
```

---

## 5. Comparación de bucles

| Bucle | Cuándo usarlo | Ventajas | Desventajas |
|-------|---------------|----------|-------------|
| `while` | Condición variable | Simple, flexible | Puede ser infinito |
| `do while` | Ejecutar al menos una vez | Garantiza una ejecución | Menos común |
| `for` (Nexis) | Rangos numéricos | Legible, seguro | Sintaxis diferente a otros lenguajes |
| `foreach` | Recorrer colecciones | Legible, seguro | No da acceso al índice |

### Cuadro comparativo

```
// WHILE (condición al inicio)
while (contador < 10) {
    // código
}

// DO WHILE (condición al final)
do {
    // código (se ejecuta al menos una vez)
} while (contador < 10)

// FOR NEXIS (rango)
for i in 0 .. 10 {
    // código
}

// FOREACH (colecciones)
foreach (numero in numeros) {
    // código
}
```

---

## 6. Palabras clave en bucles

### `break`

Sale inmediatamente del bucle.

```
for i in 0 .. 10 {
    if (i == 5):
        break   // sale cuando i es 5
    
    Console.print(i)
}
// Salida: 0, 1, 2, 3, 4
```

### `continue`

Salta a la siguiente iteración.

```
for i in 0 .. 5 {
    if (i == 2):
        continue   // salta cuando i es 2
    
    Console.print(i)
}
// Salida: 0, 1, 3, 4, 5
```

### `return` (en funciones)

Sale de la función y del bucle.

```
#inject vector;

func buscar_numero(Vector<int>: numeros, int: objetivo) -> bool {
    foreach (numero in numeros) {
        if (numero == objetivo):
            emit -> true   // sale de la función
    }
    emit -> false
}
```

---

## 7. Errores comunes

### Error 1: Bucle infinito sin control

```
int i = 0
while (i < 5) {
    Console.print(i)
    // falta i = i + 1 → bucle infinito
}
```

**Solución:** Siempre actualizar la variable de control.

```
while (i < 5) {
    Console.print(i)
    i = i + 1
}
```

### Error 2: Rango incorrecto en for

```
for i in 10 .. 0 {   // correcto (descendente)
    Console.print(i)
}
```

**Solución:** El rango siempre es inclusivo y funciona en ambos sentidos.

```
for i in 0 .. 10 {   // ascendente
    Console.print(i)
}

for i in 10 .. 0 {   // descendente
    Console.print(i)
}
```

### Error 3: Usar foreach y modificar la colección

```
foreach (numero in numeros) {
    numeros.add(10)   // error: modificar durante iteración
}
```

**Solución:** No modificar la colección mientras se itera.

### Error 4: Olvidar `step` para pasos personalizados

```
// Incorrecto (no funciona así)
for i in 0 .. 10 + 2 {
    // no es un paso, es sumar 2 al límite
}

// Correcto
for i in 0 .. 10 step 2 {
    // i toma valores: 0, 2, 4, 6, 8, 10
}
```

---

## 8. Buenas prácticas

1. **Elige el bucle adecuado:** Usa `for` para rangos numéricos, `foreach` para colecciones.

2. **Evita bucles infinitos:** Asegúrate de que la condición eventualmente sea falsa.

3. **Usa nombres descriptivos:** `i`, `j`, `k` para índices; `item`, `valor` para elementos.

4. **Mantén el bloque pequeño:** Si el bucle es muy largo, considera extraerlo a una función.

5. **Usa `break` y `continue` con moderación:** Pueden hacer el código menos legible.

6. **Prefiere `foreach` sobre `for`:** Cuando sea posible, `foreach` es más legible y seguro.

7. **Inicializa variables antes del bucle:** Si necesitas el valor después, asegúrate de inicializarlas.

8. **Usa `step` para pasos personalizados:** Facilita la lectura de iteraciones con incrementos diferentes.