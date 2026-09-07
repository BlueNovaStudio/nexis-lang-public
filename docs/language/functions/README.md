# ⚙️ Funciones en Nexis

Las funciones permiten agrupar código reutilizable. En Nexis hay dos familias: funciones **con retorno** (`func ... -> tipo`) y funciones **sin retorno** (`void`), también llamadas procedimientos.

## Contenido

- [Funciones con retorno](funtions.md) — `func`, retorno implícito y `emit ->`.
- [Funciones sin retorno](return-values.md) — `void` y parámetros opcionales.

## En esta sección aprenderás

- Definir y llamar funciones.
- Retornar valores de forma implícita o con `emit ->`.
- Usar parámetros y valores por defecto.
- Comprender el alcance (scope) y la recursión.

## Referencia rápida

```nexis
// Función con retorno (una línea: retorno implícito)
func suma(int: a, int: b) -> int {
    a + b
}

// Función con retorno (varias líneas: emit)
func es_mayor(int: edad) -> bool {
    if edad >= 18 {
        emit -> true
    } else {
        emit -> false
    }
}

// Procedimiento (sin retorno)
void saludar(string: nombre) {
    Console.print("Hola, " + nombre)
}

// Llamadas
int resultado = suma(5, 3)
bool mayor = es_mayor(20)
saludar("Ana")
```

## Parámetros

Los parámetros se escriben con el formato `tipo: nombre`:

```nexis
func ordenar(int: a, float: b, string: c) -> void
```

## Flujo recomendado

1. Aprende a definir funciones con retorno.
2. Luego practica procedimientos `void`.
3. Avanza a parámetros opcionales, scope y recursión.

> Nexis permite funciones recursivas (por ejemplo `factorial`), siempre que tengan un caso base (ver NX92). Los errores de funciones (NX30–NX35) están en el [catálogo de errores](../errors/errors.md).