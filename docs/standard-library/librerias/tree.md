# Librería Tree en Nexis

Proporciona el árbol `Tree<T>`, usado para organizar datos jerárquicamente.

## Importación

```
#inject tree;
```

## Declaración y uso

```
Tree<int> jerarquia = Tree()
jerarquia.insertar(50)
jerarquia.insertar(25)
jerarquia.insertar(75)
```

## Operaciones principales

- `insertar(valor)` agrega un valor.
- `buscar(valor)` comprueba si existe.
- `eliminar(valor)` elimina un valor.
- `en_orden()` recorre los valores ordenados.

Consulta [la documentación completa de Tree](../collections/tree.md).
