# Librería Math en Nexis

La librería `math` ofrece constantes y funciones para cálculos numéricos.

## 1. Importación

```
#inject math;
```

## 2. Constantes

| Nombre | Descripción |
|--------|-------------|
| `PI` | Relación entre la circunferencia y su diámetro |
| `E` | Base de los logaritmos naturales |

## 3. Funciones

| Función | Descripción |
|---------|-------------|
| `abs(valor)` | Valor absoluto |
| `sqrt(valor)` | Raíz cuadrada |
| `pow(base, exponente)` | Potencia |
| `min(a, b)` | Menor de dos valores |
| `max(a, b)` | Mayor de dos valores |
| `round(valor)` | Redondeo al entero más cercano |
| `floor(valor)` | Redondeo hacia abajo |
| `ceil(valor)` | Redondeo hacia arriba |
| `sin(angulo)` | Seno en radianes |
| `cos(angulo)` | Coseno en radianes |
| `tan(angulo)` | Tangente en radianes |
| `log(valor)` | Logaritmo natural |

## 4. Ejemplo

```
#inject math;

float radio = 5.0
float area = math.PI * math.pow(radio, 2)
float raiz = math.sqrt(81)
```

## 5. Errores comunes

`math.sqrt(valor)` debe recibir un valor no negativo en el dominio real. Las funciones trigonométricas reciben radianes.
