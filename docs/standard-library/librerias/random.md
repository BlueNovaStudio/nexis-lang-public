# Librería Random en Nexis

La librería `random` genera valores pseudoaleatorios para simulaciones, juegos y pruebas.

## 1. Importación

```
#inject random;
```

## 2. Funciones

| Función | Descripción |
|---------|-------------|
| `semilla(valor)` | Inicializa el generador |
| `entero(minimo, maximo)` | Entero dentro del intervalo |
| `decimal(minimo, maximo)` | Decimal dentro del intervalo |
| `eleccion(valores)` | Elemento aleatorio de un vector |
| `barajar(valores)` | Mezcla un vector |

## 3. Ejemplo

```
#inject random;

int dado = random.entero(1, 6)
Vector<string> colores = ["rojo", "azul", "verde"]
string color = random.eleccion(colores)
random.barajar(colores)
```

`random` no debe utilizarse para contraseñas, tokens ni otros valores de seguridad. Para ello se necesitará una API criptográficamente segura.
