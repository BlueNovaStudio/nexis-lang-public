# Librería File en Nexis

La librería `file` permite consultar, crear, leer y modificar archivos del sistema.

## 1. Importación

```
#inject file;
```

## 2. Funciones

| Función | Descripción |
|---------|-------------|
| `existe(ruta)` | Comprueba si existe un archivo |
| `leer(ruta)` | Devuelve todo el contenido como `string` |
| `escribir(ruta, contenido)` | Crea o reemplaza un archivo |
| `agregar(ruta, contenido)` | Añade contenido al final |
| `eliminar(ruta)` | Elimina un archivo |
| `crear_directorio(ruta)` | Crea un directorio |
| `listar_directorio(ruta)` | Devuelve sus entradas |

## 3. Ejemplo

```
#inject file;

file.escribir("datos.txt", "Nexis")
string contenido = file.leer("datos.txt")
file.agregar("datos.txt", "\nLenguaje")
```

## 4. Errores

Las operaciones deben informar si la ruta no existe, no hay permisos o el archivo no puede abrirse. No se deben eliminar archivos sin una ruta explícita.
