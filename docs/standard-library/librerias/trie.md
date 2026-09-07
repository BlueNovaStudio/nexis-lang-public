# Librería Trie en Nexis

Proporciona `Trie`, una estructura especializada en prefijos de cadenas.

## Importación

```
#inject trie;
```

## Declaración y uso

```
Trie diccionario = Trie()
diccionario.insertar("programa")
bool existe = diccionario.contiene("programa")
```

## Operaciones principales

- `insertar(palabra)` guarda una palabra.
- `contiene(palabra)` comprueba una palabra completa.
- `comienza_con(prefijo)` comprueba un prefijo.
- `buscar_prefijo(prefijo)` devuelve coincidencias.

Consulta [la documentación completa de Trie](../collections/trie.md).
