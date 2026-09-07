# Librería Time en Nexis

La librería `time` trabaja con fechas, horas y mediciones de duración.

## 1. Importación

```
#inject time;
```

## 2. Funciones

| Función | Descripción |
|---------|-------------|
| `ahora()` | Fecha y hora actual |
| `hoy()` | Fecha actual |
| `formatear(fecha, patron)` | Convierte una fecha a texto |
| `parsear(texto, patron)` | Convierte texto a fecha |
| `esperar(milisegundos)` | Pausa la ejecución |
| `reloj()` | Tiempo transcurrido desde el inicio del programa |

## 3. Ejemplo

```
#inject time;

auto inicio = time.reloj()
// Operaciones del programa
int duracion = time.reloj() - inicio
string fecha = time.formatear(time.ahora(), "YYYY-MM-DD")
```

`reloj()` debe usar una fuente monotónica para medir duraciones. `ahora()` representa el tiempo del sistema y puede cambiar.
