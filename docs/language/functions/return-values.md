# 📘 Funciones sin Retorno en Nexis

## Introducción

Las funciones sin retorno (también llamadas **procedimientos**) ejecutan un bloque de código pero **no devuelven ningún valor**. Se utilizan para realizar acciones como mostrar información, modificar variables o ejecutar procesos sin necesidad de obtener un resultado.

---

## 1. Sintaxis básica

```
void nombre_funcion(parametros) {
    // bloque de código
}
```

### Reglas importantes

- La función se declara con la palabra clave `func` (implícita) o con `void` para indicar que no retorna valor.
- Los parámetros se escriben con el formato `nombre: tipo`.
- No se usa `-> tipo_retorno` porque no hay valor de retorno.
- No se usa `emit` porque no se retorna nada.
- El bloque de código se ejecuta cuando se llama a la función.

---

## 2. Ejemplos de funciones sin retorno

### Ejemplo 1: Función básica

```
void suma(int: a, int: b) {
    Console.print(a + b)
}
```

**Uso:**
```
suma(3, 5)   // imprime 8
```

---

### Ejemplo 2: Función con múltiples operaciones

```
void mostrar_info(string: nombre, int: edad) {
    Console.print("Nombre: " + nombre)
    Console.print("Edad: " + edad)
    
    if edad >= 18 {
        Console.print("Es mayor de edad")
    } else {
        Console.print("Es menor de edad")
    }
}
```

**Uso:**
```
mostrar_info("Ana", 20)
```

**Salida:**
```
Nombre: Ana
Edad: 20
Es mayor de edad
```

---

### Ejemplo 3: Función con operaciones aritméticas

```
void calcular_y_mostrar(int: x, int: y) {
    int suma = x + y
    int resta = x - y
    int multiplicacion = x * y
    
    Console.print("Suma: " + suma)
    Console.print("Resta: " + resta)
    Console.print("Multiplicación: " + multiplicacion)
}
```

**Uso:**
```
calcular_y_mostrar(10, 5)
```

**Salida:**
```
Suma: 15
Resta: 5
Multiplicación: 50
```

---

### Ejemplo 4: Función con entrada de usuario

```
void saludar_usuario() {
    auto nombre = Console.input(text="Ingrese su nombre: ")
    Console.print("¡Hola, " + nombre + "! Bienvenido a Nexis")
}
```

**Uso:**
```
saludar_usuario()
```

**Interacción:**
```
Ingrese su nombre: Carlos
¡Hola, Carlos! Bienvenido a Nexis
```

---

### Ejemplo 5: Función con modificador de variables (por referencia)

```
void incrementar(int: numero) {
    numero = numero + 1
}
```

**Uso:**
```
int contador = 5
incrementar(contador)
Console.print(contador)   // 6
```

---

## 3. Comparación con funciones con retorno

| Característica | Sin retorno (`void`) | Con retorno |
|----------------|----------------------|-------------|
| Palabra clave | `void` | `func` + `-> tipo` |
| Retorna valor | No | Sí |
| Usa `emit` | No | Sí (en múltiples líneas) |
| Se puede asignar | No | Sí |
| Uso principal | Acciones, efectos secundarios | Cálculos, obtener valores |

### Ejemplo comparativo

**Sin retorno:**
```
void mostrar_suma(int: a, int: b) {
    Console.print(a + b)
}
```

**Con retorno:**
```
func suma(int: a, int: b) -> int {
    a + b
}
```

**Diferencia en el uso:**
```
mostrar_suma(5, 3)           // imprime 8

int resultado = suma(5, 3)   // resultado = 8
Console.print(resultado)     // imprime 8
```

---

## 4. Llamada a funciones sin retorno

Las funciones sin retorno se llaman por su nombre y se pasan los argumentos entre paréntesis.

```
// Función definida
void mostrar_mensaje(string: mensaje) {
    Console.print(mensaje)
}

// Llamada a la función
mostrar_mensaje("Hola mundo")
```

También se pueden llamar dentro de otras funciones:

```
void proceso_completo() {
    mostrar_mensaje("Iniciando proceso...")
    // otras operaciones
    mostrar_mensaje("Proceso finalizado")
}
```

---

## 5. Funciones sin retorno con parámetros opcionales

```
void mostrar_datos(string: nombre, int: edad = 18) {
    Console.print("Nombre: " + nombre)
    Console.print("Edad: " + edad)
}
```

**Uso:**
```
mostrar_datos("Ana", 25)   // Edad: 25
mostrar_datos("Luis")      // Edad: 18 (valor por defecto)
```

---

## 6. Errores comunes

### Error 1: Intentar asignar el resultado de una función void

```
int resultado = mostrar_suma(5, 3)   // error: void no retorna valor
```

**Solución:** No asignar el resultado de funciones void.

```
mostrar_suma(5, 3)   // llamada directa
```

---

### Error 2: Usar `emit` en una función void

```
void mostrar_suma(int: a, int: b) {
    emit -> a + b   // error: void no debe retornar
}
```

**Solución:** Eliminar `emit` y solo ejecutar las acciones necesarias.

```
void mostrar_suma(int: a, int: b) {
    Console.print(a + b)
}
```

---

### Error 3: Olvidar el tipo `void`

```
func suma(int: a, int: b) {   // falta void
    Console.print(a + b)
}
```

**Solución:** Especificar `void` para indicar que no retorna valor.

```
void suma(int: a, int: b) {
    Console.print(a + b)
}
```

---

## 7. Buenas prácticas

1. **Usa nombres descriptivos:** El nombre debe indicar la acción que realiza.

```
void mostrar_resultado()
void procesar_datos()
void guardar_informacion()
```

2. **Mantén funciones enfocadas:** Una función void debe hacer una sola tarea.

3. **Usa `void` explícitamente:** Aunque en Nexis se puede omitir, es recomendable usarlo para claridad.

4. **Documenta efectos secundarios:** Si la función modifica variables globales, indícalo en comentarios.

5. **Prefiere funciones con retorno para cálculos:** Si necesitas un valor, usa funciones con retorno en lugar de modificar variables globales.
