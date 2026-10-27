# Librería Random en Nexis

La librería `random` genera valores pseudoaleatorios para simulaciones,
juegos y pruebas.

## 1. Importación

```
#inject random;
```

## 2. Funciones implementadas

| Función | Parámetros | Devuelve | Descripción |
|---------|------------|----------|-------------|
| `integer(minimo, maximo)` / `entero` | `int`, `int` | `int` | Entero en `[minimo, maximo]`. |

### Comportamiento

- El intervalo es **inclusivo** en ambos extremos.
- Si `maximo < minimo`, devuelve `minimo`.
- El generador es pseudoaleatorio y determinista para una misma
  secuencia de llamadas dentro del proceso.
- No es criptográficamente seguro.

## 3. Ejemplo: lanzar un dado

```
#inject random;

for i in 1 .. 6 {
    int dado = random.integer(1, 6)
    Console.println("Tirada " + i + ": " + dado)
}
```

## 4. Ejemplo: elegir un elemento

La elección aleatoria de un vector se puede construir con
`random.integer` y el índice:

```
#inject random;
#inject Vector;

Vector<string> colores = ["rojo", "azul", "verde"]
int indice = random.integer(0, colores.length() - 1)
Console.println(colores[indice])
```

## 5. Ejemplo: barajar manualmente (Fisher-Yates)

```
#inject random;
#inject Vector;

Vector<int> cartas = [1, 2, 3, 4, 5]
for i in (cartas.length() - 1) .. 1 step -1 {
    int j = random.integer(0, i)
    int aux = cartas[i]
    cartas[i] = cartas[j]
    cartas[j] = aux
}
Console.println(cartas)
```

## 6. Funciones reservadas (no disponibles en V0.0.6)

La API planificada incluye, pero **todavía no implementa**:

- `seed` / `semilla`
- `decimal` / `decimal`
- `choice` / `eleccion`
- `shuffle` / `barajar`

## 7. Seguridad

No uses `random` para contraseñas, tokens ni claves. Para seguridad se
necesitará una API criptográficamente segura, que no forma parte de
V0.0.6.
