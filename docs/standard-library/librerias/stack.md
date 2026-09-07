# Librería Stack en Nexis

Proporciona la pila `Stack<T>`, una colección con comportamiento LIFO.

## Importación

```
#inject stack;
```

## Declaración y uso

```
Stack<string> historial = Stack()
historial.apilar("inicio")
string pantalla = historial.desapilar()
```

## Operaciones principales

- `apilar(valor)` agrega en la cima.
- `desapilar()` elimina y devuelve la cima.
- `cima()` consulta la cima sin eliminarla.
- `esta_vacia()` y `longitud()` consultan el estado.

Consulta [la documentación completa de Stack](../collections/stack.md).
