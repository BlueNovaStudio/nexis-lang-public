# Vector en Nexis

## Introducción

`Vector<T>` es una estructura dinámica que almacena elementos del mismo tipo. Puede crecer o reducir su tamaño automáticamente.


## 1. Importación de la librería

Para usar vectores, importa la librería correspondiente:

```
#inject vector;
```


## 2. Declaración

### Sintaxis

```
Vector<tipo> nombre;
```

### Ejemplo

```
Vector<int> nums = []
```

### Inicialización con valores

```
Vector<int> nums = [1, 2, 3, 4]
```

### Ejemplo completo

```
#inject vector;

Vector<int> numeros = []
numeros = [10, 20, 30, 40]

// O en una sola línea
Vector<int> datos = [5, 10, 15, 20]
```


## 3. Métodos del vector

### `agregar(valor)`
Agrega un elemento al final del vector.

```
nums.agregar(5)
nums.agregar(10)
// Resultado: [1, 2, 3, 4, 5, 10]
```


### `insertar(indice, valor)`
Inserta un elemento en una posición específica.

```
nums.insertar(0, 6)   // Inserta 6 al inicio
// Resultado: [6, 1, 2, 3, 4]
```


### `obtener(indice)`
Obtiene el elemento en una posición específica.

```
int valor = nums.obtener(2)   // Obtiene el elemento en la posición 2
Console.print(valor)      // Muestra el valor
```


### `asignar(indice, valor)`
Modifica el elemento en una posición específica.

```
nums.asignar(3, 2)   // Cambia el elemento en la posición 3 por 2
// Resultado: [1, 2, 3, 2, 4]
```


### `eliminar(indice)`
Elimina el elemento en una posición específica.

```
nums.eliminar(2)   // Elimina el elemento en la posición 2
// Resultado: [1, 2, 4]
```


### `extraer()`
Elimina y devuelve el último elemento del vector.

```
int ultimo = nums.extraer()
// ultimo = 4
// Resultado: [1, 2, 3]
```


### `contiene(valor)`
Verifica si un elemento existe en el vector.

```
bool existe = nums.contiene(3)   // true
bool existe = nums.contiene(10)  // false
```


### `ordenar()`
Ordena los elementos del vector en orden ascendente.

```
nums.ordenar()
// Resultado: [1, 2, 3, 4]
```


### `invertir()`
Invierte el orden de los elementos del vector.

```
nums.invertir()
// Resultado: [4, 3, 2, 1]
```


### `longitud()`
Devuelve el número de elementos del vector.

```
int total = nums.longitud()
Console.print(total)   // Muestra la cantidad de elementos
```


## 4. Métodos adicionales

### `limpiar()`
Elimina todos los elementos del vector.

```
nums.limpiar()
// Resultado: []
```

### `esta_vacio()`
Verifica si el vector está vacío.

```
bool vacio = nums.esta_vacio()
```

### `primero()`
Obtiene el primer elemento del vector.

```
int primero = nums.primero()
```

### `ultimo()`
Obtiene el último elemento del vector.

```
int ultimo = nums.ultimo()
```

### `indice_de(valor)`
Obtiene la posición de la primera ocurrencia de un valor.

```
int posicion = nums.indice_de(3)
// Si no existe, devuelve -1
```

### `ultimo_indice_de(valor)`
Obtiene la posición de la última ocurrencia de un valor.

```
int posicion = nums.ultimo_indice_de(3)
```


## 5. Ejemplos completos

### Ejemplo 1: Operaciones básicas con vectores

```
#inject vector;

Vector<int> numeros = [10, 20, 30, 40]

Console.print("Longitud: " + numeros.longitud())   // 4

numeros.agregar(50)                              // [10, 20, 30, 40, 50]
numeros.insertar(2, 25)                          // [10, 20, 25, 30, 40, 50]

int valor = numeros.obtener(3)                  // 30
Console.print("Valor en posición 3: " + valor)

numeros.asignar(1, 15)                           // [10, 15, 25, 30, 40, 50]
numeros.eliminar(0)                              // [15, 25, 30, 40, 50]

int ultimo = numeros.extraer()                   // 50
Console.print("Último: " + ultimo)               // Último: 50
```

### Ejemplo 2: Buscar y ordenar

```
#inject vector;

Vector<int> edades = [25, 18, 30, 22, 19]

bool contiene = edades.contiene(22)              // true
int posicion = edades.indice_de(30)              // 2

edades.ordenar()                                 // [18, 19, 22, 25, 30]
edades.invertir()                                // [30, 25, 22, 19, 18]

int total = edades.longitud()                    // 5

foreach (edad in edades) {
    Console.print(edad)
}
```

### Ejemplo 3: Uso con entrada de usuario

```
#inject vector;

Vector<string> nombres = []

while (true) {
    auto nombre = Console.input(text="Ingrese un nombre (o 'salir' para terminar): ")
    
    if (nombre == "salir"):
        break
    
    nombres.agregar(nombre)
}

Console.print("Nombres ingresados: " + nombres.longitud())

foreach (nombre in nombres) {
    Console.print("- " + nombre)
}
```


## 6. Comparación entre métodos

| Método | Descripción | Complejidad |
|--------|-------------|-------------|
| `agregar(valor)` | Agrega al final | O(1) amortizado |
| `insertar(indice, valor)` | Inserta en posición | O(n) |
| `obtener(indice)` | Obtiene por posición | O(1) |
| `asignar(indice, valor)` | Modifica por posición | O(1) |
| `eliminar(indice)` | Elimina por posición | O(n) |
| `extraer()` | Elimina el último | O(1) |
| `contiene(valor)` | Verifica existencia | O(n) |
| `ordenar()` | Ordena los elementos | O(n log n) |
| `invertir()` | Invierte el orden | O(n) |
| `longitud()` | Obtiene longitud | O(1) |


## 7. Errores comunes

### Error 1: No importar la librería

```
Vector<int> nums = []   // error: falta importar vector
```

**Solución:** Importar la librería antes de usar.

```
#inject vector;
Vector<int> nums = []
```


### Error 2: Índice fuera de rango

```
Vector<int> nums = [1, 2, 3]
int valor = nums.obtener(5)   // error: índice fuera de rango
```

**Solución:** Verificar que el índice sea menor que `longitud()`.
```
if (5 < nums.longitud()):
    int valor = nums.obtener(5)
else:
    Console.print("Índice inválido")
```


### Error 3: Usar métodos en variable no declarada como vector

```
int nums = [1, 2, 3]
nums.agregar(4)   // error: agregar no es un método de int
```

**Solución:** Declarar la variable como vector.

```
Vector<int> nums = [1, 2, 3]
nums.agregar(4)
```