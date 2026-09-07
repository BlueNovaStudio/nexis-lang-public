# 📘 Funciones con Retorno en Nexis

## Introducción

Las funciones con retorno permiten ejecutar un bloque de código y devolver un resultado. En Nexis, el valor retornado puede ser utilizado en otras operaciones o asignado a variables.

---

## 1. Sintaxis básica

```
func nombre_funcion(parametros) -> tipo_retorno {
    // bloque de código
    valor_retorno
}
```

### Reglas importantes

- La función se declara con la palabra clave `func`.
- Los parámetros se escriben con el formato `nombre: tipo`.
- El tipo de retorno se especifica después de `->`.
- Si el bloque tiene **una sola línea**, el valor se retorna implícitamente (sin usar `emit`).
- Si el bloque tiene **más de una línea**, se debe usar `emit ->` para retornar el valor.

---

## 2. Ejemplos de funciones con retorno

### Ejemplo 1: Función simple (una línea)

```
func suma(int: a, int: b) -> int {
    a + b
}
```

**Uso:**
```
int resultado = suma(5, 3)
Console.print(resultado)   // 8
```

---

### Ejemplo 2: Función con múltiples líneas (usando `emit`)

```
func suma() -> int {
    int a = 4
    int b = 3
    
    emit -> a + b
}
```

**Uso:**
```
int resultado = suma()
Console.print(resultado)   // 7
```

---

### Ejemplo 3: Función con operaciones adicionales

```
func calcular_precio(float: precio_base, float: impuesto) -> float {
    float total = precio_base + (precio_base * impuesto)
    float descuento = 5.0f
    
    if total > 100.0f {
        total = total - descuento
    }
    
    emit -> total
}
```

**Uso:**
```
float precio_final = calcular_precio(100.0f, 0.18f)
Console.print(precio_final)   // 113.0 (100 + 18 - 5)
```

---

### Ejemplo 4: Función con retorno booleano

```
func es_mayor_de_edad(int: edad) -> bool {
    if edad >= 18 {
        emit -> true
    } else {
        emit -> false
    }
}
```

**Uso:**
```
bool mayor = es_mayor_de_edad(20)
Console.print(mayor)   // true
```

---

### Ejemplo 5: Función con retorno de string

```
func saludo(string: nombre) -> string {
    string mensaje = "Hola, " + nombre + "!"
    emit -> mensaje
}
```

**Uso:**
```
auto saludo_personal = saludo("Ana")
Console.print(saludo_personal)   // "Hola, Ana!"
```

---

## 3. Comparación entre retorno implícito y `emit`

| Característica | Retorno implícito | Con `emit ->` |
|----------------|-------------------|---------------|
| Número de líneas | Una sola línea | Una o más líneas |
| Sintaxis | `valor` | `emit -> valor` |
| Uso recomendado | Funciones simples | Funciones con lógica compleja |

### Ejemplos comparativos

**Retorno implícito (una línea):**
```
func cuadrado(int: x) -> int {
    x * x
}
```

**Con `emit` (múltiples líneas):**
```
func cuadrado(int: x) -> int {
    int resultado = x * x
    emit -> resultado
}
```

---

## 4. Asignación del resultado a una variable

El valor retornado por una función puede ser almacenado en una variable.

```
int resultado = suma(10, 5)
Console.print(resultado)   // 15
```

También se puede usar directamente en expresiones:

```
int total = suma(5, 3) * 2
Console.print(total)   // 16
```

---

## 5. Funciones con retorno y entrada de usuario

```
func obtener_edad() -> int {
    int edad = Console.input(text="Ingrese su edad: ")
    emit -> edad
}

int edad_usuario = obtener_edad()
Console.print("Tu edad es: " + edad_usuario)
```

---

## 6. Errores comunes

### Error 1: Olvidar el tipo de retorno

```
func suma(int: a, int: b) {   // falta -> int
    a + b
}
```

**Solución:** Especificar el tipo de retorno con `-> tipo`.

```
func suma(int: a, int: b) -> int {
    a + b
}
```

---

### Error 2: Usar `emit` en una función de una sola línea

```
func suma(int: a, int: b) -> int {
    emit -> a + b   // no es necesario
}
```

**Solución:** Usar retorno implícito.

```
func suma(int: a, int: b) -> int {
    a + b
}
```

---

### Error 3: No retornar un valor en todas las rutas

```
func es_par(int: numero) -> bool {
    if numero % 2 == 0 {
        emit -> true
    }
    // falta retorno para cuando es impar
}
```

**Solución:** Asegurar que todas las rutas tengan un retorno.

```
func es_par(int: numero) -> bool {
    if numero % 2 == 0 {
        emit -> true
    } else {
        emit -> false
    }
}
```

---

## 7. Buenas prácticas

1. **Usa nombres descriptivos:** El nombre de la función debe indicar qué hace y qué retorna.

```
func calcular_promedio(float: a, float: b) -> float
```

2. **Mantén funciones pequeñas:** Una función debe hacer una sola cosa y hacerla bien.

3. **Prefiere retorno implícito para funciones simples:** Si la función tiene una sola línea, no uses `emit`.

4. **Usa `emit` para claridad:** En funciones complejas, `emit` hace explícito qué valor se retorna.

5. **Documenta el tipo de retorno:** Especifica siempre el tipo después de `->`.