# Pila (Stack) en Nexis

Una `Stack<T>` almacena elementos con la regla LIFO: el último elemento que entra es el primero que sale.

## 1. Importación

```
#inject stack;
```

## 2. Declaración

```
Stack<string> historial = Stack()
```

## 3. Métodos

### `apilar(valor)`
Agrega un elemento en la parte superior.

```
historial.apilar("pantalla_inicio")
historial.apilar("pantalla_ajustes")
```

### `desapilar()`
Elimina y devuelve el elemento superior.

```
string pantalla = historial.desapilar()
```

### `cima()`
Devuelve el elemento superior sin eliminarlo.

```
string actual = historial.cima()
```

### `esta_vacia()` y `longitud()`
Consultan si la pila está vacía y cuántos elementos contiene.

```
bool vacia = historial.esta_vacia()
int total = historial.longitud()
```

## 4. Ejemplo completo

```
#inject stack;

Stack<string> historial = Stack()
historial.apilar("inicio")
historial.apilar("ajustes")

while (!historial.esta_vacia()) {
	Console.print(historial.desapilar())
}
```

## 5. Complejidad

| Método | Complejidad |
|--------|-------------|
| `apilar(valor)` | O(1) |
| `desapilar()` | O(1) |
| `cima()` | O(1) |
| `esta_vacia()` | O(1) |
| `longitud()` | O(1) |

## 6. Error común

No se puede declarar una pila sin indicar el tipo de sus elementos:

```
Stack historial = Stack()   // error
```

Usa `Stack<T>` y asegúrate de importar `stack`.
