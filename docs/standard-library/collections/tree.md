# Árbol (Tree) en Nexis

Un `Tree<T>` organiza datos jerárquicamente. En un árbol binario de búsqueda, los valores menores quedan a la izquierda y los mayores a la derecha.

## 1. Importación

```
#inject tree;
```

## 2. Declaración

```
Tree<int> jerarquia = Tree()
```

## 3. Métodos

### `insertar(valor)`
Inserta un valor respetando el orden del árbol.

### `buscar(valor)`
Devuelve `true` si el valor existe.

### `eliminar(valor)`
Elimina un valor del árbol.

### `en_orden()`
Recorre los valores de menor a mayor.

```
jerarquia.insertar(50)
jerarquia.insertar(25)
jerarquia.insertar(75)
bool existe = jerarquia.buscar(25)
jerarquia.en_orden()
```

## 4. Ejemplo completo

```
#inject tree;

Tree<int> jerarquia = Tree()
jerarquia.insertar(50)
jerarquia.insertar(25)
jerarquia.insertar(75)
jerarquia.insertar(10)
jerarquia.eliminar(25)
```

## 5. Complejidad

| Método | Promedio | Peor caso |
|--------|----------|-----------|
| `insertar(valor)` | O(log n) | O(n) |
| `buscar(valor)` | O(log n) | O(n) |
| `eliminar(valor)` | O(log n) | O(n) |
| `en_orden()` | O(n) | O(n) |
