# Librería Graphics en Nexis

La librería `graphics` proporciona una API para ventanas, escenas y dibujo. Su implementación dependerá del motor gráfico elegido para Nexis.

## 1. Importación

```
#inject graphics;
```

## 2. Funciones

| Función | Descripción |
|---------|-------------|
| `crear_ventana(ancho, alto, titulo)` | Crea una ventana |
| `limpiar(color)` | Limpia el lienzo |
| `punto(x, y, color)` | Dibuja un punto |
| `linea(x1, y1, x2, y2, color)` | Dibuja una línea |
| `rectangulo(x, y, ancho, alto, color)` | Dibuja un rectángulo |
| `texto(x, y, contenido, tamano)` | Dibuja texto |
| `mostrar()` | Presenta el cuadro actual |
| `cerrar()` | Cierra la ventana |

## 3. Ejemplo

```
#inject graphics;

graphics.crear_ventana(800, 600, "Nexis")
graphics.limpiar("negro")
graphics.rectangulo(100, 100, 200, 120, "azul")
graphics.mostrar()
graphics.cerrar()
```

Las coordenadas comienzan en la esquina superior izquierda y se expresan en píxeles.
