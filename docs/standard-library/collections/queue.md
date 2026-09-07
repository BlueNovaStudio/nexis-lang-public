# Cola (Queue) en Nexis

Una `Queue<T>` almacena elementos con la regla FIFO: el primer elemento que entra es el primero que sale.

## 1. Importación

```
#inject queue;
```

## 2. Declaración

```
Queue<int> turnos_banco = Queue()
```

## 3. Métodos

### `encolar(valor)`
Agrega un elemento al final de la cola.

### `desencolar()`
Elimina y devuelve el primer elemento.

### `frente()`
Devuelve el primer elemento sin eliminarlo.

### `esta_vacia()` y `longitud()`
Consultan el estado y el tamaño de la cola.

```
turnos_banco.encolar(101)
turnos_banco.encolar(102)
int turno = turnos_banco.desencolar()
```

## 4. Ejemplo completo

```
#inject queue;

Queue<int> turnos_banco = Queue()
turnos_banco.encolar(101)
turnos_banco.encolar(102)

while (!turnos_banco.esta_vacia()) {
	Console.print(turnos_banco.desencolar())
}
```

## 5. Complejidad

| Método | Complejidad |
|--------|-------------|
| `encolar(valor)` | O(1) |
| `desencolar()` | O(1) |
| `frente()` | O(1) |
| `esta_vacia()` | O(1) |
| `longitud()` | O(1) |
