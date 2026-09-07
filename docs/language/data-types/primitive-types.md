# 🧱 Tipos primitivos en Nexis

Los tipos primitivos son los bloques básicos con los que se construye cualquier programa. Nexis soporta números, texto y valores booleanos.

## Tabla de tipos primitivos

| Tipo | Descripción | Ejemplo de valor | Uso típico |
|------|-------------|------------------|------------|
| `int` | Número entero | `42`, `-7`, `0` | Conteos, índices, operaciones exactas |
| `float` | Decimal de precisión simple (sufijo `f`) | `3.14f`, `1.4f` | Mediciones ligeras |
| `double` | Decimal de precisión doble | `2.71828`, `2500.99` | Cálculos que requieren precisión |
| `char` | Un solo carácter (comillas simples) | `'A'`, `'z'`, `'7'` | Símbolos, letras individuales |
| `string` | Cadena de texto (comillas dobles) | `"Hola"`, `"Lima"` | Texto, mensajes |
| `bool` | Valor booleano | `true`, `false` | Condiciones, flags |
| `const` | Modificador: valor inmutable | `const double PI = 3.14159` | Constantes físicas, configuración |
| `auto` | Inferencia de tipo | `auto n = 10` | Código conciso (debe inicializar) |

## Detalle por tipo

### `int`

Enteros con signo. Se usan para contar, indexar y operar exactamente.

```nexis
int edad = 25
int contador = 0
int temperatura = -5
```

> La división entre enteros (`a / b`) devuelve un entero. Usa `float` o `double` si necesitas decimales.

### `float` y `double`

Números con parte decimal. `float` usa el sufijo `f`; `double` no requiere sufijo.

```nexis
float altura = 1.4f
float precio = 99.99f
double sueldo = 1500.50
double precision = 3.141592653589793
```

### `char`

Un solo carácter entre comillas simples (`' '`). No confundir con `string`.

```nexis
char letra = 'A'
char signo = '+'  // 'A' es char; "+" sería string
```

### `string`

Texto entre comillas dobles (`" "`). Se concatenan con `+` y se manipulan con la librería `string`.

```nexis
string nombre = "Ana"
string saludo = "Hola, " + nombre   // "Hola, Ana"
```

### `bool`

Solo acepta `true` o `false`. Es el resultado de las comparaciones y los operadores lógicos.

```nexis
bool activo = true
bool mayor = edad >= 18
bool combo = mayor && tienePermiso
```

## Modificadores

### `const`

Declara un valor que **no se puede modificar** después de su inicialización. Debe inicializarse en la misma línea.

```nexis
const double PI = 3.14159
const int DIAS_SEMANA = 7
```

Intentar reasignar una constante produce el error [NX03](../errors/errors.md#nx03-reasignación-de-constante). Declararla sin valor produce [NX06](../errors/errors.md#nx06-constante-sin-inicializar).

### `auto`

Deduce el tipo a partir del valor asignado. Exige inicializar en la misma línea.

```nexis
auto n = 16          // int
auto nombre = "Carlos"   // string
auto altura = 1.75   // double
auto activo = true   // bool
```

## Conversión de tipos

Nexis es de tipado estático: no convierte automáticamente tipos incompatibles (error [NX07](../errors/errors.md#nx07-tipo-incompatible-en-asignación)). Usa conversión explícita cuando sea necesario:

```nexis
string texto = "20"
int edad = int(texto)      // convierte string a int

int x = 5
string etiqueta = string(x)   // convierte int a string
```

### Resumen

- Los números (`int`, `float`, `double`) soportan operadores aritméticos.
- La concatenación de texto usa `+` entre `string`.
- Las comparaciones devuelven `bool`.
- Los errores de tipo más comunes son NX07, NX10 y NX12. Consúltalos en el [catálogo de errores](../errors/errors.md).