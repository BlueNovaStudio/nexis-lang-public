# 🔀 Control de flujo en Nexis

El control de flujo permite decidir qué bloques de código se ejecutan y cuántas veces, en función de condiciones y repeticiones.

## Contenido

- [Condicionales](conditionals.md) — `if`, `else if`, `else`, ternario y `switch`.
- [Bucles](loops.md) — `while`, `do while`, `for` y `foreach`.

## En esta sección aprenderás

- Tomar decisiones con dos estilos de sintaxis (llaves o `:`).
- Repetir código con rangos numéricos y colecciones.
- Usar `break`, `continue` y `emit ->` dentro de bucles.

## Referencia rápida

```nexis
// Condicional
if (edad >= 18) {
    Console.print("Mayor de edad")
} else {
    Console.print("Menor de edad")
}

// Switch con rango
switch (nota) {
    case 90 ... 100:
        Console.print("Excelente")
    break
    default:
        Console.print("Regular")
}

// Bucles
for i in 0 .. 10 {
    Console.print(i)
}

foreach (nombre in nombres) {
    Console.print("Hola, " + nombre)
}
```

## Flujo recomendado

1. Aprende los condicionales (dos estilos + `switch`).
2. Practica los bucles (rangos y colecciones).
3. Combina ambos para resolver problemas reales.

> Los errores de control de flujo (NX20–NX24) están documentados en el [catálogo de errores](../errors/errors.md).