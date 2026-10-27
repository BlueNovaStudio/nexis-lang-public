# Librería Time en Nexis

La librería `time` permite medir duraciones dentro de un programa.

## 1. Importación

```
#inject time;
```

## 2. Funciones implementadas

| Función | Parámetros | Devuelve | Descripción |
|---------|------------|----------|-------------|
| `clock()` / `reloj` | — | `int` | Milisegundos desde el inicio del programa. |

### Comportamiento

- `clock` usa una fuente monotónica: siempre avanza, nunca retrocede.
- Devuelve un entero de milisegundos.
- Es ideal para medir el tiempo de un algoritmo, no para obtener la hora
  del día.

## 3. Ejemplo: medir un algoritmo

```
#inject time;
#inject Vector;

Vector<int> datos = []
for i in 0 ... 10000 {
    datos.add(i)
}

int inicio = time.clock()

datos.sort()

int fin = time.clock()
Console.println("Ordenar tardó " + (fin - inicio) + " ms")
```

## 4. Ejemplo: cronómetro simple

```
#inject time;

int inicio = time.clock()

// ... trabajo ...

int transcurrido = time.clock() - inicio
if (transcurrido > 1000) {
    Console.println("El proceso tardó más de un segundo")
}
```

## 5. Funciones reservadas (no disponibles en V0.0.6)

La API planificada incluye, pero **todavía no implementa**:

- `now` / `ahora` (fecha y hora actual)
- `today` / `hoy`
- `format` / `formatear`
- `parse` / `parsear`
- `sleep` / `esperar`

Estas funciones requieren un modelo de fecha y zona horaria que se
incorporará en una versión posterior.

## 6. Errores comunes

| Error | Solución |
|-------|----------|
| Esperar la hora del sistema con `clock` | Usar `clock` solo para duraciones. |
| Comparar relojes de procesos distintos | No son comparables. |
| Llamar `time.now()` en V0.0.6 | No está implementada. |
