# 📘 Manejo de Excepciones (Try/Catch) en Nexis

## Introducción

El manejo de excepciones permite controlar errores en tiempo de ejecución de manera estructurada. Nexis ofrece un sistema completo de `try/catch/finally` que permite capturar, gestionar y depurar errores de forma profesional.

---

## 1. Sintaxis básica

```
try {
    // Código que puede lanzar un error
} catch (ErrorTipo e) {
    // Manejar el error específico
} catch (Error e) {
    // Manejar cualquier otro error
} finally {
    // Código que siempre se ejecuta (haya o no error)
}
```

### Características

- `try`: Bloque donde se ejecuta el código que puede fallar.
- `catch`: Captura y maneja errores específicos.
- `finally`: Se ejecuta siempre, ideal para liberar recursos.
- Los bloques `catch` se evalúan en orden (del más específico al más general).

---

## 2. Ejemplo básico

```
#inject vector;

try {
    Vector<int> datos = [10, 20]
    Console.print(datos.obtener(5))   // Error: índice fuera de rango
} catch (ErrorIndice e) {
    Console.print("Te saliste del límite: " + e.mensaje())
} catch (Error e) {
    Console.print("Algo salió mal: " + e.codigo())
} finally {
    Console.print("Esto se ejecuta SIEMPRE, falle o no.")
}
```

---

## 3. Lanzar errores (throw)

Puedes lanzar errores intencionalmente usando la palabra clave `lanzar` (o `throw`).

### Sintaxis

```
lanzar ErrorTipo("mensaje descriptivo")
```

### Ejemplo

```
func dividir(int: a, int: b) -> int {
    if (b == 0):
        lanzar ErrorMatematico("División por cero")
    
    emit -> a / b
}

try {
    int resultado = dividir(10, 0)
    Console.print(resultado)
} catch (ErrorMatematico e) {
    Console.print("Error matemático: " + e.mensaje())
}
```

---

## 4. Relanzar errores

Puedes capturar un error y volver a lanzarlo si no puedes manejarlo en ese nivel.

```
try {
    // Código que puede fallar
} catch (Error e) {
    Console.print("Fallo detectado, registrando error...")
    lanzar e   // Relanza el mismo error
}
```

---

## 5. Métodos del objeto Error (`e`)

Cuando capturas un error, el objeto `e` proporciona métodos para obtener información detallada.

### `e.mensaje()`
Retorna un string con el texto descriptivo del error.

```
catch (Error e) {
    Console.print("Error: " + e.mensaje())
}
```

### `e.codigo()`
Retorna un número entero con el código del error.

```
catch (Error e) {
    Console.print("Código de error: " + e.codigo())
}
```

### `e.tipo()`
Retorna el nombre de la clase del error.

```
catch (Error e) {
    Console.print("Tipo de error: " + e.tipo())
}
```

### `e.linea()`
Retorna el número de línea donde ocurrió el error.

```
catch (Error e) {
    Console.print("Línea: " + e.linea())
}
```

### `e.archivo()`
Retorna el nombre del archivo donde ocurrió el error.

```
catch (Error e) {
    Console.print("Archivo: " + e.archivo())
}
```

### `e.traza_pila()`
Retorna un vector con el stack trace (cadena de llamadas).

```
catch (Error e) {
    vector traza = e.traza_pila()
    Console.print("Stack trace:")
    foreach (item in traza) {
        Console.print("  " + item)
    }
}
```

### `e.causa()`
Retorna el error original si este fue causado por otro error.

```
catch (Error e) {
    Error causa = e.causa()
    if (causa != null):
        Console.print("Causado por: " + causa.mensaje())
}
```

---

## 6. Ejemplo completo con todos los métodos

```
try {
    Vector<int> datos = [10, 20]
    datos.obtener(5)   // Error: índice fuera de rango
} catch (ErrorIndice e) {
    Console.print("--- DETALLES DEL ERROR ---")
    Console.print("Mensaje: " + e.mensaje())
    Console.print("Código: " + e.codigo())
    Console.print("Tipo: " + e.tipo())
    Console.print("Línea: " + e.linea())
    Console.print("Archivo: " + e.archivo())
    
    Console.print("Stack trace:")
    foreach (item in e.traza_pila()) {
        Console.print("  " + item)
    }
    
    Error causa = e.causa()
    if (causa != null):
        Console.print("Causa original: " + causa.mensaje())
} finally {
    Console.print("Bloque finally ejecutado.")
}
```

---

## 7. Funciones útiles para errores

### `imprimir_error(texto)`
Envía el mensaje a la salida de errores (stderr).

```
catch (Error e) {
    imprimir_error("Error crítico: " + e.mensaje())
}
```

### `terminar(codigo)`
Aborta la ejecución del programa con un código de salida.

```
catch (ErrorCritico e) {
    imprimir_error("Error fatal. Cerrando programa.")
    terminar(1)   // 1 = fallo
}
```

### `afirmar(condicion, mensaje)`
Lanza un error si la condición es falsa.

```
try {
    Vector<int> datos = [10, 20]
    afirmar(datos.longitud() > 0, "El vector está vacío")
    Console.print("Vector válido")
} catch (ErrorAssert e) {
    Console.print("Assert falló: " + e.mensaje())
}
```

---

## 8. Tipos de errores comunes

Cada tipo de excepción se corresponde con uno o varios **códigos NX** del [catálogo de errores](errors.md). Úsalos como referencia para saber qué capturar.

| Tipo de error | Código NX | Descripción |
|---------------|-----------|-------------|
| `ErrorIndice` | NX11 | Índice fuera de rango en vectores o colecciones |
| `ErrorDivision` | NX01 | División por cero |
| `ErrorMatematico` | NX01, NX13 | Operación matemática fuera de dominio |
| `ErrorTipo` | NX07, NX10 | Error de tipo de dato |
| `ErrorValidacion` | NX12, NX60 | Validación de datos fallida |
| `ErrorMemoria` | NX92 | Problemas de memoria |
| `ErrorArchivo` | NX61, NX62 | Error al leer/escribir archivos |
| `ErrorEntrada` | NX60 | Error en la entrada del usuario |
| `ErrorRed` | NX70 | Problemas de red o conexión |
| `ErrorGrafico` | NX71 | Error en operaciones gráficas |
| `ErrorAssert` | NX44 | Fallo en `afirmar()` |

> 💡 Cuando un error no se captura (código `NX42`), el programa aborta y muestra el código NX de la causa, la línea y el archivo.

---

## 9. Errores comunes

### Error 1: Capturar antes de lanzar

```
catch (Error e) {
    // Hacer algo
}
lanzar Error("Nuevo error")   // error: lanzar fuera de try
```

**Solución:** `lanzar` solo dentro de `try` o funciones que lo contengan.

---

### Error 2: No manejar errores específicos primero

```
try {
    // código
} catch (Error e) {
    // Maneja todo
} catch (ErrorIndice e) {   // error: nunca se ejecutará
    // Maneja solo índices
}
```

**Solución:** Capturar errores específicos antes del general.

```
try {
    // código
} catch (ErrorIndice e) {
    // Maneja índices
} catch (Error e) {
    // Maneja el resto
}
```

---

### Error 3: No usar `finally` para liberar recursos

```
try {
    // Abrir archivo
} catch (Error e) {
    Console.print("Error")
}
// El archivo puede quedar abierto
```

**Solución:** Usar `finally` para liberar recursos.

```
try {
    // Abrir archivo
} catch (Error e) {
    Console.print("Error")
} finally {
    // Cerrar archivo
}
```

---

## 10. Buenas prácticas

1. **Captura errores específicos primero:** Siempre coloca los `catch` de errores más específicos antes de los genéricos.

2. **Usa `finally` para limpiar recursos:** Cierra archivos, conexiones o libera memoria en `finally`.

3. **Proporciona mensajes claros:** Los mensajes de error deben ayudar a depurar.

4. **No abuses de `catch` general:** Capturar `Error` sin más oculta problemas.

5. **Documenta qué errores puede lanzar una función:** Ayuda a quienes usen tu código.

6. **Usa `imprimir_error` para errores críticos:** Separa la salida normal de los errores.

7. **Relanza cuando no puedas manejar el error:** No los ignores silenciosamente.

8. **Usa `afirmar` para validar condiciones:** Es una forma rápida de detectar fallos temprano.