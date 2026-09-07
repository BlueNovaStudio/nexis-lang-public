# ➕ Operadores en Nexis

Los operadores permiten calcular, comparar y tomar decisiones. Nexis los organiza en categorías.

## Contenido

- [Operadores](operadores.md) — aritméticos, asignación, comparación, lógicos, ternario y precedencia.

## En esta sección aprenderás

- Realizar cálculos con operadores aritméticos y de asignación.
- Comparar valores y combinar condiciones.
- Usar el operador ternario `=>` ... `<-->`.
- Respetar la precedencia de operadores.

## Referencia rápida

```nexis
int a = 10
int b = 3

int suma = a + b          // 13
int division = a / b      // 3 (división entera)
int modulo = a % b        // 1
int potencia = a ** b     // 1000

a += 5                    // a = 15

bool igual = a == b        // false
bool mayor = a > b         // true
bool combo = (a > b) && (b < 5)

string estado = (edad >= 18) => "Mayor" <--> "Menor"
```

> Los errores de operadores (NX01, NX07, NX10, NX13) están documentados en el [catálogo de errores](../errors/errors.md).