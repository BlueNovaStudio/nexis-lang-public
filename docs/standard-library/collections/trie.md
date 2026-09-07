# Trie en Nexis

Un `Trie` organiza cadenas por prefijos. Es útil para búsquedas rápidas, autocompletado y diccionarios.

## 1. Importación

```
#inject trie;
```

## 2. Declaración

Un `Trie` trabaja con cadenas por definición, por lo que no necesita un parámetro de tipo.

```
Trie diccionario_autocompletado = Trie()
```

## 3. Métodos

### `insertar(palabra)`
Guarda una palabra en el árbol de prefijos.

### `contiene(palabra)`
Comprueba si una palabra completa está almacenada.

### `comienza_con(prefijo)`
Comprueba si existe alguna palabra con ese prefijo.

### `buscar_prefijo(prefijo)`
Devuelve las palabras que comienzan con el prefijo.

```
diccionario_autocompletado.insertar("programacion")
diccionario_autocompletado.insertar("programa")
bool existe = diccionario_autocompletado.contiene("programa")
```

## 4. Ejemplo completo

```
#inject trie;

Trie diccionario_autocompletado = Trie()
diccionario_autocompletado.insertar("programacion")
diccionario_autocompletado.insertar("programa")
diccionario_autocompletado.insertar("programador")
bool coincide = diccionario_autocompletado.comienza_con("pro")
```

## 5. Complejidad

Sea $L$ la longitud de la palabra o prefijo consultado.

| Método | Complejidad |
|--------|-------------|
| `insertar(palabra)` | O(L) |
| `contiene(palabra)` | O(L) |
| `comienza_con(prefijo)` | O(L) |
| `buscar_prefijo(prefijo)` | O(L + k) |

`k` representa la cantidad de resultados devueltos.
