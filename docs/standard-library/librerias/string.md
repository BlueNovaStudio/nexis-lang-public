# Librería String en Nexis

La librería `string` permite consultar, transformar y dividir cadenas de texto.

## 1. Importación

```
#inject string;
```

## 2. Funciones

| Función | Descripción |
|---------|-------------|
| `longitud(texto)` | Cantidad de caracteres |
| `mayusculas(texto)` | Convierte a mayúsculas |
| `minusculas(texto)` | Convierte a minúsculas |
| `recortar(texto)` | Elimina espacios de los extremos |
| `contiene(texto, fragmento)` | Comprueba si existe un fragmento |
| `comienza_con(texto, prefijo)` | Comprueba el prefijo |
| `termina_con(texto, sufijo)` | Comprueba el sufijo |
| `reemplazar(texto, origen, destino)` | Sustituye coincidencias |
| `dividir(texto, separador)` | Devuelve un vector de partes |
| `unir(partes, separador)` | Une un vector de cadenas |
| `subcadena(texto, inicio, cantidad)` | Extrae una parte |
| `indice_de(texto, fragmento)` | Primera posición o `-1` |

## 3. Ejemplo

```
#inject string;

string nombre = "  Nexis  "
string limpio = string.recortar(nombre)
string titulo = string.mayusculas(limpio)
Vector<string> palabras = string.dividir("uno,dos,tres", ",")
```

## 4. Complejidad

Para una cadena de longitud $n$, las operaciones de búsqueda y transformación normalmente cuestan O(n).
