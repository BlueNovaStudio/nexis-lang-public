# Librería Linked List en Nexis

Proporciona la lista enlazada `LinkedList<T>`, formada por nodos independientes.

## Importación

```
#inject linked_list;
```

## Declaración y uso

```
LinkedList<float> temperaturas = LinkedList()
temperaturas.agregar_frente(36.5)
temperaturas.agregar_fondo(37.2)
```

## Operaciones principales

- `agregar_frente(valor)` inserta al inicio.
- `agregar_fondo(valor)` inserta al final.
- `eliminar_frente()` elimina el primer nodo.
- `obtener(indice)` y `longitud()` consultan la lista.

Consulta [la documentación completa de Linked List](../collections/linked_list.md).
