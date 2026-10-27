# Librería Trie en Nexis

`Trie` es un árbol de prefijos especializado en **cadenas**. Permite
insertar palabras y consultar si una palabra o un prefijo existe.

## 1. Importación

```
#inject Trie;
```

## 2. Declaración e inicialización

```
Trie vacio = Trie()
Trie diccionario = Trie()
diccionario.insert("programa")
diccionario.insert("programar")
diccionario.insert("programacion")
```

`Trie` no lleva parámetro de tipo: siempre almacena cadenas.

## 3. Métodos

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `insert(palabra)` / `insertar` | `string` | `void` | Guarda una palabra. |
| `contains(palabra)` / `contiene` | `string` | `bool` | `true` si la palabra completa existe. |
| `startsWith(prefijo)` / `comienza_con` | `string` | `bool` | `true` si algún elemento empieza por el prefijo. |
| `searchPrefix(prefijo)` / `buscar_prefijo` | `string` | `Vector<string>` | Palabras que empiezan por el prefijo. |

## 4. Ejemplo completo

```
#inject Trie;
#inject Vector;

Trie diccionario = Trie()
diccionario.insert("casa")
diccionario.insert("casamiento")
diccionario.insert("casual")
diccionario.insert("perro")

Console.println(diccionario.contains("casa"))       // true
Console.println(diccionario.contains("cas"))        // false (no es palabra completa)
Console.println(diccionario.startsWith("cas"))      // true

Vector<string> coincidencias = diccionario.searchPrefix("cas")
foreach (palabra in coincidencias) {
    Console.println(palabra)
}
// casa
// casamiento
// casual
```

## 5. Autocompletado

```
#inject Trie;
#inject Vector;

Trie palabras = Trie()
palabras.insert("Nexis")
palabras.insert("Nexo")
palabras.insert("Nube")

Vector<string> sugerencias = palabras.searchPrefix("Ne")
foreach (s in sugerencias) {
    Console.println(s)
}
// Nexis
// Nexo
```

## 6. Errores comunes

| Error | Código | Solución |
|-------|--------|----------|
| Esperar búsqueda por substring | — | `Trie` busca por **prefijo**, no en el medio. |
| Confundir `contains` con `startsWith` | — | `contains` exige la palabra completa. |
| Pasar un no-string | `NX07` | Convertir con `string(...)` o usar texto. |

## 7. Complejidad

Insertar y buscar una palabra de longitud `m` cuesta O(m).
`searchPrefix` cuesta O(m + k), donde `k` son las coincidencias.
