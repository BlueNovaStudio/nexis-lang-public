# Librería Graphics en Nexis

La librería `graphics` está **reservada** para ventanas, escenas y
dibujo. En V0.0.6 **no hay funciones implementadas**: cualquier llamada
devuelve `void`.

## 1. Importación

```
#inject graphics;
```

## 2. Estado en V0.0.6

| Función planificada | Estado |
|---------------------|--------|
| `createWindow(ancho, alto, titulo)` | No implementada |
| `clear(color)` | No implementada |
| `point(x, y, color)` | No implementada |
| `line(x1, y1, x2, y2, color)` | No implementada |
| `rectangle(x, y, ancho, alto, color)` | No implementada |
| `text(x, y, contenido, tamano)` | No implementada |
| `present()` | No implementada |
| `close()` | No implementada |

## 3. Alternativa en V0.0.6

La salida gráfica se puede aproximar con arte ASCII usando
`Console.println` y bucles:

```
int ancho = 20
int alto = 10
for y in 0 ... alto {
    string fila = ""
    for x in 0 ... ancho {
        if (x == 0 || x == ancho - 1 || y == 0 || y == alto - 1) {
            fila = fila + "#"
        } else {
            fila = fila + " "
        }
    }
    Console.println(fila)
}
```

## 4. Diseño previsto

Cuando se implemente, la API deberá:

- abrir una ventana con tamaño y título;
- dibujar primitivas (punto, línea, rectángulo, texto);
- presentar el cuadro y cerrar limpiamente;
- usar coordenadas en píxeles desde la esquina superior izquierda.

## 5. Errores comunes

| Error | Solución |
|-------|----------|
| Esperar que se abra una ventana | No está implementado en V0.0.6. |
| Asignar el resultado de `graphics.*` | Devuelve `void`. |

Este documento se actualizará cuando la librería esté disponible.
