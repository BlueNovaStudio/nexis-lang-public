# Librería Queue en Nexis

Proporciona la cola `Queue<T>`, una colección con comportamiento FIFO.

## Importación

```
#inject queue;
```

## Declaración y uso

```
Queue<int> turnos = Queue()
turnos.encolar(101)
int turno = turnos.desencolar()
```

## Operaciones principales

- `encolar(valor)` agrega al final.
- `desencolar()` elimina y devuelve el frente.
- `frente()` consulta el primer elemento.
- `esta_vacia()` y `longitud()` consultan el estado.

Consulta [la documentación completa de Queue](../collections/queue.md).
