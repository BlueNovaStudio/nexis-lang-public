# Librería File en Nexis

La librería `file` permite comprobar, leer y escribir archivos del
sistema.

## 1. Importación

```
#inject file;
```

## 2. Funciones implementadas

| Función | Parámetros | Devuelve | Descripción |
|---------|------------|----------|-------------|
| `exists(ruta)` / `existe` | `string` | `bool` | Comprueba si la ruta existe. |
| `read(ruta)` / `leer` | `string` | `string` | Lee todo el contenido. |
| `write(ruta, contenido)` / `escribir` | `string`, `string` | `void` | Crea o reemplaza el archivo. |

### Comportamiento

- `read` lanza `NX61` (`ErrorArchivo`) si el archivo no existe o no se
  puede leer.
- `write` lanza `NX62` (`ErrorArchivo`) si no se puede escribir (permisos,
  ruta inválida, disco lleno).
- `write` **reemplaza** todo el contenido anterior.
- Las rutas son relativas al directorio desde el que se ejecuta el
  programa, salvo que se use una ruta absoluta.

## 3. Ejemplo completo

```
#inject file;

string ruta = "datos.txt"

if (!file.exists(ruta)) {
    file.write(ruta, "Nexis")
}

string contenido = file.read(ruta)
Console.println(contenido)

file.write(ruta, contenido + "\nLenguaje")
Console.println(file.read(ruta))
```

## 4. Ejemplo: leer y procesar un archivo

```
#inject file;
#inject string;
#inject Vector;

if (file.exists("numeros.txt")) {
    string texto = file.read("numeros.txt")
    Vector<string> lineas = string.split(texto, "\n")

    int suma = 0
    foreach (linea in lineas) {
        if (string.trim(linea) != "") {
            suma = suma + int(linea)
        }
    }
    Console.println("Suma: " + suma)
}
```

## 5. Manejo de errores

```
#inject file;

try {
    string datos = file.read("no_existe.txt")
    Console.println(datos)
} catch (ErrorArchivo e) {
    Console.println("No se pudo leer: " + e.mensaje())
}
```

## 6. Funciones reservadas (no disponibles en V0.0.6)

La API planificada incluye, pero **todavía no implementa**:

- `append` / `agregar` (añadir al final)
- `remove` / `eliminar`
- `createDirectory` / `crear_directorio`
- `listDirectory` / `listar_directorio`

Para añadir contenido, lee el archivo, concatena y vuelve a escribirlo.

## 7. Errores comunes

| Error | Código | Solución |
|-------|--------|----------|
| Archivo inexistente al leer | `NX61` | Comprobar con `file.exists`. |
| Ruta sin permisos al escribir | `NX62` | Verificar la ruta y permisos. |
| Pérdida de datos | — | `write` reemplaza; leer antes si hay que conservar. |
