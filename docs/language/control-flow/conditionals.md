# 📘 Condicionales en Nexis

## Introducción

Los condicionales permiten ejecutar diferentes bloques de código según se cumpla o no una condición. Nexis ofrece **dos estilos de sintaxis** para adaptarse a diferentes preferencias y contextos.

---

## 1. Sintaxis estilo C/Java/JavaScript (con llaves)

### Estructura básica

```
if (condicion) {
    // código si la condición es verdadera
} else {
    // código si la condición es falsa
}
```

### Características

- Usa **llaves `{}`** para delimitar bloques de código.
- La condición va entre **paréntesis `()`**.
- Es el estilo recomendado cuando el bloque tiene **más de una línea**.
- Ocupa menos líneas que el estilo Python.

### Ejemplo 1: if-else básico

```
int edad = 18

if (edad >= 18) {
    Console.print("Eres mayor de edad.")
} else {
    Console.print("Eres menor de edad.")
}
```

### Ejemplo 2: if-else if-else

```
int nota = 85

if (nota >= 90) {
    Console.print("Sobresaliente")
} else if (nota >= 70) {
    Console.print("Aprobado")
} else {
    Console.print("Reprobado")
}
```

### Ejemplo 3: Múltiples condiciones

```
int edad = 25
bool tiene_licencia = true

if (edad >= 18 && tiene_licencia) {
    Console.print("Puede conducir")
} else {
    Console.print("No puede conducir")
}
```

---

## 2. Sintaxis estilo Python (sin llaves)

### Estructura básica

```
if (condicion):
    // código si la condición es verdadera
else:
    // código si la condición es falsa
```

### Características

- Usa **dos puntos `:`** después de la condición.
- No usa llaves `{}`.
- La indentación define los bloques de código.
- Es el estilo **recomendado cuando el bloque tiene una sola línea**.
- Es más legible para condiciones simples.

### Ejemplo 1: if-else básico (una línea)

```
int edad = 18

if (edad >= 18):
    Console.print("Eres mayor de edad.")
else:
    Console.print("Eres menor de edad.")
```

### Ejemplo 2: if-else if-else (una línea)

```
int nota = 85

if (nota >= 90):
    Console.print("Sobresaliente")
else if (nota >= 70):
    Console.print("Aprobado")
else:
    Console.print("Reprobado")
```

### Ejemplo 3: if anidado (una línea)

```
int edad = 20
bool tiene_permiso = true

if (edad >= 18):
    if (tiene_permiso):
        Console.print("Puede ingresar")
    else:
        Console.print("No tiene permiso")
else:
    Console.print("Es menor de edad")
```

---

## 3. Comparación de estilos

| Característica | Estilo C/Java/JS | Estilo Python |
|----------------|------------------|---------------|
| Delimitadores | `{}` | `:` + indentación |
| Condición | `(condicion)` | `(condicion)` |
| Uso recomendado | Múltiples líneas | Una sola línea |
| Ocupa menos líneas | Sí | No |
| Claridad en bloques largos | Mejor | Puede ser confuso |
| Claridad en bloques cortos | Puede ser verboso | Mejor |

### Ejemplo comparativo (una línea)

**Estilo Python (recomendado):**
```
if (edad >= 18):
    Console.print("Mayor de edad")
else:
    Console.print("Menor de edad")
```

**Estilo C/Java/JS (válido pero más extenso):**
```
if (edad >= 18) {
    Console.print("Mayor de edad")
} else {
    Console.print("Menor de edad")
}
```

---

## 4. Reglas para elegir el estilo

### Usar estilo Python (con `:`) cuando:

- El bloque `if`, `else if` o `else` tiene **solo una línea**.
- La condición es simple y directa.
- Se busca máxima legibilidad y minimalismo.

### Usar estilo C/Java/JS (con `{}`) cuando:

- El bloque tiene **más de una línea**.
- Hay múltiples operaciones dentro del bloque.
- Se necesita una delimitación clara de bloques extensos.

### Ejemplo mixto (recomendado)

```
int edad = 18
string nombre = "Ana"

// Estilo Python para una línea
if (edad >= 18):
    Console.print("Mayor de edad")
else:
    Console.print("Menor de edad")

// Estilo C/Java/JS para múltiples líneas
if (edad >= 18) {
    string mensaje = "Bienvenido, " + nombre
    Console.print(mensaje)
    Console.print("Puedes acceder al contenido")
    
    if (edad >= 21) {
        Console.print("También puedes acceder a la sección premium")
    }
} else {
    Console.print("Acceso denegado")
    Console.print("Debes ser mayor de edad")
}
```

---

## 5. Operador ternario

La nueva estructura se define visualmente con un símbolo de evaluación (`=>`) que conecta la condición con las opciones, y el separador bilateral (`<-->`) que representa la bifurcación exclusiva entre la opción verdadera y la falsa.

### Sintaxis estructural

```plaintext
variable_destino = (condicion_logica) => [expresion_si_verdadera] <--> [expresion_si_falsa]
```

### Análisis de los componentes

- `=>` (Operador de implicación/resolución): indica que el resultado de la condición a su izquierda determinará el camino a tomar a su derecha.
- `<-->` (Operador de exclusión mutua): actúa como un pivote visual fuerte. Deja claro que lo que está a su izquierda y a su derecha son caminos opuestos y excluyentes.

### Comportamiento y reglas de ejecución

Esta estructura debe comportarse bajo el principio de evaluación perezosa (short-circuiting):

1. **Evaluación singular:** el sistema primero resuelve únicamente la `condicion_logica`.
2. **Bifurcación verdadera:** si la condición es verdadera, se evalúa y ejecuta solo la `expresion_si_verdadera`. La expresión a la derecha de `<-->` queda completamente ignorada.
3. **Bifurcación falsa:** si la condición es falsa, se ignora la parte izquierda y se evalúa directamente `expresion_si_falsa`.

### Ejemplo 1: Asignación simple de variables

```plaintext
edad = 20
estado = (edad >= 18) => "Mayor de edad" <--> "Menor de edad"
// Resultado: estado vale "Mayor de edad"
```

### Ejemplo 2: Evitar errores críticos

```plaintext
divisor = 0
resultado = (divisor != 0) => (100 / divisor) <--> 0
// Resultado: resultado vale 0. El sistema ignoró por completo (100 / divisor).
```

### Ejemplo 3: Ejecución de procesos complejos

```plaintext
saldo_disponible = 500
costo_compra = 800

(saldo_disponible >= costo_compra) => ProcesarPago() <--> RechazarTransaccion()
// Resultado: solo se ejecuta RechazarTransaccion()
```

> Esta estructura es ideal cuando se desea una decisión condicional compacta, segura y eficiente, especialmente para evitar evaluaciones innecesarias o costosas.

---

## 6. Switch / Case

La estructura `switch` permite evaluar una variable y ejecutar diferentes bloques de código según su valor.

### Sintaxis

```
switch (variable) {
    case valor1:
        // código para valor1
    break
    case valor2:
        // código para valor2
    break
    default:
        // código si no coincide con ningún caso
}
```

### Características

- La variable se evalúa una sola vez.
- Cada `case` compara con un valor específico.
- `break` sale del bloque `switch`.
- `default` es opcional y se ejecuta cuando ningún `case` coincide.

### Ejemplo 1: Switch básico

```
int dia = 3
string nombre_dia

switch (dia) {
    case 1:
        nombre_dia = "Lunes"
    break
    case 2:
        nombre_dia = "Martes"
    break
    case 3:
        nombre_dia = "Miércoles"
    break
    case 4:
        nombre_dia = "Jueves"
    break
    case 5:
        nombre_dia = "Viernes"
    break
    case 6:
        nombre_dia = "Sábado"
    break
    case 7:
        nombre_dia = "Domingo"
    break
    default:
        nombre_dia = "Día inválido"
}

Console.print(nombre_dia)   // "Miércoles"
```

### Ejemplo 2: Switch con string

```
string comando = "guardar"

switch (comando) {
    case "guardar":
        Console.print("Guardando archivo...")
    break
    case "abrir":
        Console.print("Abriendo archivo...")
    break
    case "cerrar":
        Console.print("Cerrando archivo...")
    break
    default:
        Console.print("Comando no reconocido")
}
```

### Ejemplo 3: Switch con múltiples casos

```
string letra = "a"

switch (letra) {
    case "a":
    case "e":
    case "i":
    case "o":
    case "u":
        Console.print("Es una vocal")
    break
    default:
        Console.print("Es una consonante")
}
```

### Ejemplo 4: Switch con valores numéricos

```
int calificacion = 85
string nivel

switch (calificacion) {
    case 90 ... 100:
        nivel = "Excelente"
    break
    case 70 ... 89:
        nivel = "Aprobado"
    break
    case 50 ... 69:
        nivel = "Regular"
    break
    default:
        nivel = "Reprobado"
}

Console.print(nivel)   // "Aprobado"
```

> **Nota:** El operador `...` indica un rango de valores (inclusive).

---

## 7. Operadores en condiciones

Los condicionales pueden usar cualquier operador de comparación o lógico.

### Operadores de comparación

| Operador | Significado |
|----------|-------------|
| `==` | Igual a |
| `!=` | Diferente de |
| `>` | Mayor que |
| `<` | Menor que |
| `>=` | Mayor o igual que |
| `<=` | Menor o igual que |

### Operadores lógicos

| Operador | Significado |
|----------|-------------|
| `&&` | Y (AND) |
| `\|\|` | O (OR) |
| `!` | No (NOT) |

### Ejemplos

```
int edad = 25
float ingresos = 1500.50
bool tiene_licencia = true

// Comparaciones simples
if (edad >= 18):
    Console.print("Es mayor de edad")

// Operadores lógicos
if (edad >= 18 && ingresos >= 1000.0f):
    Console.print("Puede solicitar el crédito")

if (!tiene_licencia):
    Console.print("No tiene licencia")

// Condiciones anidadas
if (edad >= 18) {
    if (ingresos >= 1000.0f) {
        Console.print("Cumple con todos los requisitos")
    } else {
        Console.print("Cumple la edad pero no los ingresos")
    }
} else {
    Console.print("No cumple la edad mínima")
}
```

---

## 8. Errores comunes

### Error 1: Mezclar estilos incorrectamente

```
if (edad >= 18):
    Console.print("Mayor de edad")
} else {
    Console.print("Menor de edad")
}
```

**Solución:** Usar un solo estilo consistente.

---

### Error 2: Olvidar la indentación en estilo Python

```
if (edad >= 18):
Console.print("Mayor de edad")   // error: falta indentación
```

**Solución:** Indentar correctamente el bloque.

```
if (edad >= 18):
    Console.print("Mayor de edad")
```

---

### Error 3: Usar `=` en lugar de `==`

```
if (edad = 18) {   // error: asignación, no comparación
    Console.print("Edad es 18")
}
```

**Solución:** Usar `==` para comparar.

```
if (edad == 18) {
    Console.print("Edad es 18")
}
```

---

### Error 4: Olvidar los paréntesis en la condición

```
if edad >= 18 {   // error: falta paréntesis
    Console.print("Mayor de edad")
}
```

**Solución:** Siempre usar paréntesis en la condición.

```
if (edad >= 18) {
    Console.print("Mayor de edad")
}
```

---

### Error 5: Olvidar `break` en switch

```
switch (dia) {
    case 1:
        Console.print("Lunes")   // falta break
    case 2:
        Console.print("Martes")
}
```

**Solución:** Agregar `break` al final de cada caso.

```
switch (dia) {
    case 1:
        Console.print("Lunes")
    break
    case 2:
        Console.print("Martes")
    break
}
```

---

## 9. Buenas prácticas

1. **Elige un estilo y sé consistente:** No mezcles estilos en el mismo archivo sin razón.

2. **Usa estilo Python para condiciones simples:** Cuando el bloque tiene una línea, `:` es más limpio.

3. **Usa estilo C/Java/JS para bloques largos:** Las llaves `{}` ayudan a delimitar bloques extensos.

4. **Siempre usa paréntesis en la condición:** Aunque en Python no son obligatorios, en Nexis se recomienda usarlos para claridad.

5. **Indenta correctamente:** La indentación es importante en ambos estilos, especialmente en el estilo Python.

6. **Usa nombres descriptivos en las condiciones:** Las variables deben ser claras para que la condición sea legible.

7. **Usa switch para múltiples valores fijos:** Cuando tienes muchas comparaciones con valores específicos, `switch` es más legible que múltiples `else if`.

8. **Usa operador ternario solo para asignaciones simples:** Si la lógica es compleja, usa `if-else` para mayor claridad.

9. **Siempre incluye `default` en switch:** Aunque sea opcional, ayuda a manejar casos inesperados.