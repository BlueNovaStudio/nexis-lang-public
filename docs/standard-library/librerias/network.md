# Librería Network en Nexis

La librería `network` está **reservada** para comunicación HTTP y
sockets. En V0.0.6 **no hay funciones implementadas**: cualquier llamada
devuelve `void`.

## 1. Importación

```
#inject network;
```

## 2. Estado en V0.0.6

| Función planificada | Estado |
|---------------------|--------|
| `get(url)` | No implementada |
| `post(url, datos)` | No implementada |
| `openSocket(host, puerto)` | No implementada |
| `send(socket, datos)` | No implementada |
| `receive(socket, cantidad)` | No implementada |
| `close(socket)` | No implementada |

## 3. Qué hacer mientras tanto

- Usa `file` para intercambiar datos localmente.
- Para pruebas, genera los datos con `random` o léelos de un archivo.
- No incluyas credenciales en el código fuente.

## 4. Diseño previsto

Cuando se implemente, la API deberá:

- validar URLs y limitar el tamaño de las respuestas;
- permitir configurar tiempos de espera;
- usar HTTPS para datos sensibles;
- devolver errores claros (`ErrorRed`) en lugar de fallar en silencio.

## 5. Errores comunes

| Error | Solución |
|-------|----------|
| Esperar una respuesta de `network.get` | No está implementada en V0.0.6. |
| Asignar el resultado a una variable | Devuelve `void`. |

Este documento se actualizará cuando la librería esté disponible.
