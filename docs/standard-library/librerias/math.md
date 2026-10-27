# Librería Math en Nexis

La librería `math` ofrece constantes y funciones para cálculos numéricos.

## 1. Importación

```
#inject math;
```

## 2. Constantes

| Nombre | Valor | Descripción |
|--------|-------|-------------|
| `math.PI` | 3.141592653589793 | Relación entre circunferencia y diámetro. |
| `math.E` | 2.718281828459045 | Base de los logaritmos naturales. |

## 3. Funciones implementadas

| Función | Parámetros | Devuelve | Descripción |
|---------|------------|----------|-------------|
| `sqrt(x)` | numérico | `double` | Raíz cuadrada. |
| `pow(base, exponente)` | numérico, numérico | `double` | Potencia. |
| `log(x)` | numérico | `double` | Logaritmo natural (base `e`). |
| `abs(x)` | numérico | `double` | Valor absoluto. |
| `floor(x)` | numérico | `double` | Redondeo hacia abajo. |
| `ceil(x)` | numérico | `double` | Redondeo hacia arriba. |
| `round(x)` | numérico | `double` | Entero más cercano. |
| `min(a, b)` | numérico, numérico | `double` | Menor de dos valores. |
| `max(a, b)` | numérico, numérico | `double` | Mayor de dos valores. |

### Parámetros y conversión

- Todos los argumentos se convierten a número en tiempo de ejecución.
- El resultado es `double`; se puede asignar a `float`, `double` o
  convertir a `int` con `int(...)`.
- Si falta un argumento, se usa `0` (no se lanza error).

## 4. Ejemplo completo

```
#inject math;

float radio = 5.0
double area = math.PI * math.pow(radio, 2)
Console.println(area)              // 78.53981633974483

Console.println(math.sqrt(81))     // 9
Console.println(math.log(math.E))  // 1
Console.println(math.abs(-7))      // 7
Console.println(math.floor(3.9))   // 3
Console.println(math.ceil(3.1))    // 4
Console.println(math.round(3.5))   // 4
Console.println(math.min(4, 9))    // 4
Console.println(math.max(4, 9))    // 9
```

## 5. Ejemplo: distancia entre puntos

```
#inject math;

double x1 = 0.0
double y1 = 0.0
double x2 = 3.0
double y2 = 4.0

double dx = x2 - x1
double dy = y2 - y1
double distancia = math.sqrt(dx * dx + dy * dy)
Console.println(distancia)   // 5
```

## 6. Funciones reservadas (no disponibles en V0.0.6)

Las siguientes aparecen en la API planificada, pero **todavía no están
implementadas** en el runtime. Llamarlas devuelve `void`:

- `sin`, `cos`, `tan`, `asin`, `acos`, `atan`
- `log10`, `log2`
- `trunc`
- `random` (usar la librería `random`)

Se documentarán aquí cuando se implementen.

## 7. Errores comunes

| Situación | Resultado |
|-----------|-----------|
| `math.sqrt(-1)` | `NaN` (no hay error de ejecución). |
| `math.log(0)` | `-inf`. |
| `math.pow(0, -1)` | `inf`. |
| Usar `math.sin` en V0.0.6 | Devuelve `void`; no usar todavía. |

Comprueba el dominio antes de usar el resultado en una comparación.
