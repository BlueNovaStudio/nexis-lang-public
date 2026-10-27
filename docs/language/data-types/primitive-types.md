# Tipos de datos en Nexis

Los tipos de datos son los bloques básicos con los que se construye cualquier programa. Nexis soporta números (enteros y decimales), texto, valores booleanos y modificadores de tipo.

## Tabla completa de tipos primitivos

| Tipo | Descripción | Ejemplo de valor | Uso típico |
|------|-------------|------------------|------------|
| `int` | Entero con signo (32 bits) | `42`, `-7`, `0` | Conteos, índices, operaciones exactas |
| `long` | Entero largo con signo (64 bits) | `10000000000L` | Valores que exceden el rango de `int` |
| `long long` | Entero largo largo con signo (64 bits) | `9000000000000LL` | Valores extremos, IDs globales |
| `short` | Entero corto con signo (16 bits) | `100` | Valores pequeños, optimización de memoria |
| `unsigned int` | Entero sin signo (32 bits) | `4294967295u` | Conteos que nunca son negativos |
| `unsigned long` | Entero largo sin signo (64 bits) | `18446744073709551615uL` | Rangos grandes sin signo |
| `float` | Decimal de precisión simple (sufijo `f`) | `3.14f`, `1.4f` | Mediciones ligeras |
| `double` | Decimal de precisión doble | `2.71828`, `2500.99` | Cálculos que requieren precisión |
| `long double` | Decimal de precisión extendida | `1.7976931348623157e+308` | Máxima precisión disponible |
| `char` | Un solo carácter (comillas simples) | `'A'`, `'z'`, `'7'` | Símbolos, letras individuales |
| `string` | Cadena de texto (comillas dobles) | `"Hola"`, `"Lima"` | Texto, mensajes |
| `bool` | Valor booleano | `true`, `false` | Condiciones, flags |
| `const` | Modificador: valor inmutable | `const double PI = 3.14159` | Constantes físicas, configuración |
| `auto` | Inferencia de tipo | `auto n = 10` | Código conciso (debe inicializar) |

## Rango y tamaño

| Tipo | Tamaño | Rango |
|------|--------|-------|
| `short` | 2 bytes | -32,768 a 32,767 |
| `int` | 4 bytes | -2,147,483,648 a 2,147,483,647 |
| `long` | 8 bytes | -9.22 × 10¹⁸ a 9.22 × 10¹⁸ |
| `long long` | 8 bytes | -9.22 × 10¹⁸ a 9.22 × 10¹⁸ |
| `unsigned int` | 4 bytes | 0 a 4,294,967,295 |
| `unsigned long` | 8 bytes | 0 a 18.44 × 10¹⁸ |
| `float` | 4 bytes | ~7 dígitos decimales |
| `double` | 8 bytes | ~15 dígitos decimales |
| `long double` | 16 bytes | ~18–19 dígitos decimales |

## Detalle por tipo

### `int`

Enteros con signo de 32 bits. Se usan para contar, indexar y operar exactamente.

```nexis
int edad = 25
int contador = 0
int temperatura = -5
```

> La división entre enteros (`a / b`) devuelve un entero. Usa `float` o `double` si necesitas decimales.

### `long` y `long long`

Enteros de 64 bits. Úsalos cuando el valor excede el rango de `int` (> 2,147,483,647).

```nexis
long poblacion = 8000000000L
long long idGlobal = 9007199254740993LL
```

> `long` y `long long` tienen el mismo rango en Nexis (64 bits). Se mantienen ambos por compatibilidad y claridad de intención.

### `short`

Entero corto de 16 bits. Útil cuando el valor está acotado y quieres ahorrar memoria.

```nexis
short nota = 100
short mes = 12
```

### `unsigned int` y `unsigned long`

Enteros sin signo: solo aceptan valores ≥ 0. Duplican el rango positivo a cambio de no poder representar negativos.

```nexis
unsigned int maxConexiones = 4294967295u
unsigned long totalBytes = 18446744073709551615uL
```

> ⚠️ Comparar un `unsigned` con un `int` negativo produce comportamiento indefinido. Evita mezclarlos.

### `float` y `double`

Números con parte decimal. `float` usa el sufijo `f`; `double` no requiere sufijo.

```nexis
float altura = 1.4f
float precio = 99.99f
double sueldo = 1500.50
double precision = 3.141592653589793
```

### `long double`

Precisión extendida. Úsalo solo cuando `double` no basta (cálculos científicos, criptografía).

```nexis
long double constante = 1.7976931348623157e+308
```

### `char`

Un solo carácter entre comillas simples (`' '`). No confundir con `string`.

```nexis
char letra = 'A'
char signo = '+'
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
const unsigned long MAX_ID = 18446744073709551615uL
```

Intentar reasignar una constante produce el error [NX03](../errors/catalog-01-variables-y-tipos.md#nx03-reasignación-de-constante). Declararla sin valor produce [NX06](../errors/catalog-01-variables-y-tipos.md#nx06-constante-sin-inicializar).

### `auto`

Deduce el tipo a partir del valor asignado. Exige inicializar en la misma línea.

```nexis
auto n = 16            // int
auto nombre = "Carlos" // string
auto altura = 1.75     // double
auto activo = true     // bool
auto grande = 9000000000L  // long
```

## Conversión de tipos

Nexis es de tipado estático: no convierte automáticamente tipos incompatibles (error [NX07](../errors/catalog-01-variables-y-tipos.md#nx07-tipo-incompatible-en-asignación)). Usa conversión explícita cuando sea necesario:

```nexis
string texto = "20"
int edad = int(texto)           // string → int

int x = 5
string etiqueta = string(x)     // int → string

double d = 3.99
int entero = int(d)             // double → int (trunca: 3)

long l = 10000000000L
int pequeno = int(l)            // long → int (⚠️ puede truncar)

int i = 42
unsigned int ui = unsigned int(i)  // int → unsigned int
```

> ⚠️ Convertir de un tipo más grande a uno más pequeño (`long` → `int`, `double` → `int`) puede perder datos. Nexis emite una advertencia [NX12](../errors/catalog-01-variables-y-tipos.md#nx12-conversión-de-tipo-inválida).

### Resumen

- Los números enteros (`short`, `int`, `long`, `long long`) y sus variantes `unsigned` soportan operadores aritméticos.
- Los decimales (`float`, `double`, `long double`) soportan aritmética en punto flotante.
- La concatenación de texto usa `+` entre `string`.
- Las comparaciones devuelven `bool`.
- Los errores de tipo más comunes son NX07, NX10 y NX12. Consúltalos en el [catálogo de errores](../errors/errors.md).

