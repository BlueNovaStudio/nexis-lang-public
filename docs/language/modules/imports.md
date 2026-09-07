# 📘 Implementación de Librerías o Ficheros en Nexis

## Introducción

Las librerías (o bibliotecas) permiten reutilizar código, funciones y estructuras definidas en otros archivos. En Nexis, la importación se realiza mediante la directiva `#inject`, que permite incluir librerías nativas o archivos propios.

---

## 1. Sintaxis básica

Para importar una librería en Nexis, se utiliza la directiva `#inject` seguida del nombre de la librería y terminando con punto y coma (`;`).

```
#inject nombre_libreria;
```

### Características

- La directiva es `#inject`.
- **Lleva punto y coma (`;`)** al final.
- No necesita comillas ni corchetes.
- Se puede importar una o varias librerías en líneas separadas.

---

## 2. Importación de librerías nativas

### Ejemplo 1: Importar una sola librería

```
#inject vector;
```

### Ejemplo 2: Importar múltiples librerías

```
#inject vector;
#inject stack;
#inject math;
```

---

## 3. Importación de archivos propios (ficheros locales)

También es posible importar archivos creados por el usuario.

### Sintaxis

```
#inject "ruta/archivo.nex";
```

### Características

- La ruta del archivo va entre comillas dobles (`" "`).
- Se puede especificar una ruta relativa o absoluta.
- La extensión del archivo es `.nex`.

### Ejemplo 1: Importar un archivo local

```
#inject "mis_funciones.nex";
```

### Ejemplo 2: Importar desde una carpeta

```
#inject "utilidades/calculos.nex";
```

### Ejemplo 3: Importar con ruta relativa

```
#inject "../librerias/comunes.nex";
```

---

## 4. Combinación de librerías nativas y propias

```
#inject math;
#inject vector;
#inject string;
#inject file;
#inject time;
#inject random;
#inject graphics;
#inject network;
#inject "mis_funciones.nex";
#inject "utilidades/graficos.nex";
```

---

## 5. Librerías comunes en Nexis

| Librería | Descripción |
|----------|-------------|
| `math` | Funciones matemáticas (seno, coseno, raíz cuadrada, etc.) |
| `vector` | Arreglo dinámico de elementos (`Vector<T>`) |
| `stack` | Estructura de datos tipo pila (LIFO) |
| `queue` | Estructura de datos tipo cola (FIFO) |
| `set` | Conjunto de valores únicos (`Set<T>`) |
| `map` | Asociación entre claves y valores (`Map<K, V>`) |
| `linked_list` | Lista de nodos enlazados (`LinkedList<T>`) |
| `tree` | Árbol binario de búsqueda (`Tree<T>`) |
| `graph` | Grafo de vértices y conexiones (`Graph<T>`) |
| `trie` | Árbol de prefijos para cadenas (`Trie`) |
| `string` | Funciones de manipulación de cadenas |
| `file` | Lectura y escritura de archivos |
| `time` | Funciones de tiempo y fechas |
| `random` | Generación de números aleatorios |
| `graphics` | Gráficos y visualización |
| `network` | Funciones de red y comunicación |

---

## 6. Buenas prácticas

1. **Coloca las importaciones al inicio:** Todas las directivas `#inject` deben estar al principio del archivo.

2. **Una directiva por línea:** Aunque no es obligatorio, es más legible.

3. **Usa nombres claros:** Nombra tus archivos con nombres descriptivos (ej. `operaciones_matematicas.nex`).

4. **Agrupa por tipo:** Primero librerías nativas, luego archivos propios.

5. **Evita importar innecesariamente:** Solo importa lo que realmente vayas a usar.

6. **Usa rutas relativas:** Para proyectos grandes, usa rutas relativas para mayor portabilidad.