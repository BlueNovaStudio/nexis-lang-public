# Lista enlazada (Linked List) en Nexis

Una `LinkedList<T>` almacena elementos en nodos enlazados. Es útil cuando se insertan o eliminan elementos con frecuencia sin requerir memoria contigua.

## 1. Importación

```
#inject linked_list;
```

## 2. Declaración

```
LinkedList<float> temperaturas = LinkedList()
```

La notación opcional `(1 -> 2 -> 3)` puede representar una lista enlazada literal cuando el lenguaje la habilite.

## 3. Métodos

### `agregar_frente(valor)`
Inserta un nodo al inicio.

### `agregar_fondo(valor)`
Inserta un nodo al final.

### `eliminar_frente()`
Elimina y devuelve el primer elemento.

### `obtener(indice)` y `longitud()`
Acceden a un elemento por índice y consultan el tamaño de la lista.

```
temperaturas.agregar_frente(36.5)
temperaturas.agregar_fondo(37.2)
float temperatura = temperaturas.obtener(0)
```

## 4. Ejemplo completo

```
#inject linked_list;

LinkedList<float> temperaturas = LinkedList()
temperaturas.agregar_frente(36.5)
temperaturas.agregar_fondo(37.2)
temperaturas.eliminar_frente()
```

## 5. Complejidad

| Método | Complejidad |
|--------|-------------|
| `agregar_frente(valor)` | O(1) |
| `agregar_fondo(valor)` | O(1) |
| `eliminar_frente()` | O(1) |
| `obtener(indice)` | O(n) |
| `longitud()` | O(1) |
