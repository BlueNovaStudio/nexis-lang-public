# Librería Network en Nexis

La librería `network` ofrece comunicación mediante HTTP y sockets. Las operaciones de red son potencialmente lentas y deben permitir errores y tiempos de espera.

## 1. Importación

```
#inject network;
```

## 2. Funciones

| Función | Descripción |
|---------|-------------|
| `get(url)` | Realiza una petición HTTP GET |
| `post(url, datos)` | Envía datos mediante HTTP POST |
| `abrir_socket(host, puerto)` | Abre una conexión TCP |
| `enviar(socket, datos)` | Envía bytes o texto |
| `recibir(socket, cantidad)` | Recibe datos |
| `cerrar(socket)` | Cierra la conexión |

## 3. Ejemplo

```
#inject network;

auto respuesta = network.get("https://nexis.dev/api/version")
Console.print(respuesta.estado)
Console.print(respuesta.cuerpo)
```

## 4. Seguridad

La librería debe validar URLs, limitar tamaños de respuesta y permitir configurar un tiempo de espera. Para datos sensibles se debe usar HTTPS y evitar incluir credenciales en el código fuente.
