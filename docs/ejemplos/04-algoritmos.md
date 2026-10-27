# 🧮 Algoritmos clásicos en Nexis

Primera parte de algoritmos con código ejecutable: **ordenamientos** y
**búsquedas**. La segunda (recursión, matrices, cadenas y matemáticas) continúa
en [07-algoritmos-avanzado.md](07-algoritmos-avanzado.md).

Todos los ejemplos usan solo lo que Nexis V0.0.6 implementa. Las firmas de las
colecciones están en la [referencia rápida](../referencia-rapida.md).

---

## 1. Ordenamiento

### 1.1 Burbuja (bubble sort)

Compara pares adyacentes y sube el mayor al final. La bandera `cambio` corta
antes si el vector ya está ordenado.

```nexis
#inject Vector;

void burbuja(Vector<int>: v) -> void {
    int n = v.length()
    bool cambio = true
    int pasada = 0
    while (cambio && pasada < n - 1) {
        cambio = false
        for i in 0 ... n - 1 - pasada {
            if (v[i] > v[i + 1]) {
                int tmp = v[i]
                v[i] = v[i + 1]
                v[i + 1] = tmp
                cambio = true
            }
        }
        pasada = pasada + 1
    }
}

Vector<int> datos = [5, 1, 4, 2, 8, 0, 2]
burbuja(datos)
Console.println(datos)
```

Salida:

```
[0, 1, 2, 2, 4, 5, 8]
```

### 1.2 Selección (selection sort)

Busca el mínimo de la parte no ordenada y lo coloca al principio.

```nexis
#inject Vector;

void seleccion(Vector<int>: v) -> void {
    int n = v.length()
    for i in 0 ... n - 1 {
        int minimo = i
        for j in i + 1 ... n {
            if (v[j] < v[minimo]) {
                minimo = j
            }
        }
        if (minimo != i) {
            int tmp = v[i]
            v[i] = v[minimo]
            v[minimo] = tmp
        }
    }
}

Vector<int> datos = [64, 25, 12, 22, 11]
seleccion(datos)
Console.println(datos)
```

Salida:

```
[11, 12, 22, 25, 64]
```

### 1.3 Inserción (insertion sort)

Inserta cada elemento en su lugar dentro de la parte ya ordenada. Es muy
rápido con vectores casi ordenados.

```nexis
#inject Vector;

void insercion(Vector<int>: v) -> void {
    for i in 1 ... v.length() {
        int clave = v[i]
        int j = i - 1
        while (j >= 0 && v[j] > clave) {
            v[j + 1] = v[j]
            j = j - 1
        }
        v[j + 1] = clave
    }
}

Vector<int> datos = [9, 5, 1, 4, 3]
insercion(datos)
Console.println(datos)

Vector<int> casi = [1, 2, 4, 3, 5]
insercion(casi)
Console.println(casi)
```

Salida:

```
[1, 3, 4, 5, 9]
[1, 2, 3, 4, 5]
```

### 1.4 Quick sort

Elige el último elemento como pivote, particiona y recursa en ambos lados.
Como las funciones reciben las colecciones con copia de salida, los cambios
vuelven al llamador en cada nivel.

```nexis
#inject Vector;

void quick(Vector<int>: v, int bajo, int alto) -> void {
    if (bajo < alto) {
        int pivote = v[alto]
        int i = bajo - 1

        for j in bajo ... alto {
            if (v[j] <= pivote) {
                i = i + 1
                int tmp = v[i]
                v[i] = v[j]
                v[j] = tmp
            }
        }

        int tmp2 = v[i + 1]
        v[i + 1] = v[alto]
        v[alto] = tmp2

        int p = i + 1
        quick(v, bajo, p - 1)
        quick(v, p + 1, alto)
    }
}

Vector<int> datos = [10, 7, 8, 9, 1, 5]
quick(datos, 0, datos.length() - 1)
Console.println(datos)
```

Salida:

```
[1, 5, 7, 8, 9, 10]
```

### 1.5 Merge sort

Divide a la mitad, ordena cada mitad y fusiona. Necesita un vector auxiliar
`temp` para la mezcla.

```nexis
#inject Vector;

void mezclar(Vector<int>: v, int izq, int medio, int der) -> void {
    Vector<int> temp = []
    int i = izq
    int j = medio + 1

    while (i <= medio && j <= der) {
        if (v[i] <= v[j]) {
            temp.add(v[i])
            i = i + 1
        } else {
            temp.add(v[j])
            j = j + 1
        }
    }
    while (i <= medio) {
        temp.add(v[i])
        i = i + 1
    }
    while (j <= der) {
        temp.add(v[j])
        j = j + 1
    }

    for k in 0 ... temp.length() {
        v[izq + k] = temp[k]
    }
}

void merge_sort(Vector<int>: v, int izq, int der) -> void {
    if (izq < der) {
        int medio = (izq + der) / 2
        merge_sort(v, izq, medio)
        merge_sort(v, medio + 1, der)
        mezclar(v, izq, medio, der)
    }
}

Vector<int> datos = [38, 27, 43, 3, 9, 82, 10]
merge_sort(datos, 0, datos.length() - 1)
Console.println(datos)
```

Salida:

```
[3, 9, 10, 27, 38, 43, 82]
```

### 1.6 Counting sort (enteros no negativos)

Cuenta cuántas veces aparece cada valor y reconstruye el vector. Es O(n + k),
pero solo sirve para enteros en un rango conocido.

```nexis
#inject Vector;

void counting_sort(Vector<int>: v) -> void {
    if (v.isEmpty()) {
        // nada que ordenar
    } else {
        int maximo = v[0]
        foreach (n in v) {
            if (n > maximo) {
                maximo = n
            }
        }

        Vector<int> conteo = []
        for i in 0 .. maximo {
            conteo.add(0)
        }

        foreach (n in v) {
            conteo[n] = conteo[n] + 1
        }

        int pos = 0
        for valor in 0 .. maximo {
            for veces in 0 ... conteo[valor] {
                v[pos] = valor
                pos = pos + 1
            }
        }
    }
}

Vector<int> datos = [4, 2, 2, 8, 3, 3, 1]
counting_sort(datos)
Console.println(datos)
```

Salida:

```
[1, 2, 2, 3, 3, 4, 8]
```

### 1.7 El ordenamiento incorporado

Para el día a día, `Vector.sort()` ordena en el lugar y `reverse()` invierte.

```nexis
#inject Vector;

Vector<int> datos = [5, 1, 4, 2, 3]
datos.sort()
Console.println(datos)
datos.reverse()
Console.println(datos)

Vector<string> nombres = ["Luis", "Ana", "Eva"]
nombres.sort()
Console.println(nombres)
```

Salida:

```
[1, 2, 3, 4, 5]
[5, 4, 3, 2, 1]
[Ana, Eva, Luis]
```

### 1.8 Comparación

| Algoritmo | Mejor | Promedio | Peor | Memoria | ¿Estable? |
|-----------|-------|----------|------|---------|-----------|
| Burbuja | O(n) | O(n²) | O(n²) | O(1) | Sí |
| Selección | O(n²) | O(n²) | O(n²) | O(1) | No |
| Inserción | O(n) | O(n²) | O(n²) | O(1) | Sí |
| Quick sort | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| Merge sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Sí |
| Counting sort | O(n + k) | O(n + k) | O(n + k) | O(k) | Sí |
| `Vector.sort()` | — | O(n log n) | O(n log n) | O(log n) | No |

---

## 2. Búsqueda

### 2.1 Búsqueda lineal

Recorre hasta encontrar el valor. Funciona con cualquier vector, ordenado o no.

```nexis
#inject Vector;

func lineal(Vector<int>: v, int: objetivo) -> int {
    for i in 0 ... v.length() {
        if (v[i] == objetivo) {
            emit -> i
        }
    }
    emit -> -1
}

Vector<int> datos = [10, 20, 30, 40]
Console.println(lineal(datos, 30))
Console.println(lineal(datos, 99))
```

Salida:

```
2
-1
```

### 2.2 Búsqueda binaria iterativa

Requiere el vector **ordenado**. Descarta la mitad en cada paso.

```nexis
#inject Vector;

func binaria(Vector<int>: v, int: objetivo) -> int {
    int bajo = 0
    int alto = v.length() - 1
    int encontrado = -1
    bool seguir = true

    while (seguir && bajo <= alto) {
        int medio = (bajo + alto) / 2
        if (v[medio] == objetivo) {
            encontrado = medio
            seguir = false
        } else if (v[medio] < objetivo) {
            bajo = medio + 1
        } else {
            alto = medio - 1
        }
    }

    emit -> encontrado
}

Vector<int> ordenado = [1, 3, 5, 7, 9, 11, 13]
Console.println(binaria(ordenado, 7))
Console.println(binaria(ordenado, 1))
Console.println(binaria(ordenado, 13))
Console.println(binaria(ordenado, 4))
```

Salida:

```
3
0
6
-1
```

### 2.3 Búsqueda binaria recursiva

```nexis
#inject Vector;

func binaria_rec(Vector<int>: v, int: objetivo, int: bajo, int: alto) -> int {
    if (bajo > alto) {
        emit -> -1
    }

    int medio = (bajo + alto) / 2
    if (v[medio] == objetivo) {
        emit -> medio
    }
    if (v[medio] < objetivo) {
        emit -> binaria_rec(v, objetivo, medio + 1, alto)
    }
    emit -> binaria_rec(v, objetivo, bajo, medio - 1)
}

Vector<int> ordenado = [2, 4, 6, 8, 10, 12]
Console.println(binaria_rec(ordenado, 10, 0, ordenado.length() - 1))
Console.println(binaria_rec(ordenado, 5, 0, ordenado.length() - 1))
```

Salida:

```
4
-1
```

### 2.4 Búsqueda de texto

`Vector.indexOf` ya hace búsqueda lineal de un elemento y `Trie` resuelve
prefijos en tiempo proporcional a la palabra.

```nexis
#inject Vector;
#inject Trie;

Vector<string> nombres = ["Ana", "Luis", "Eva"]
Console.println(nombres.indexOf("Luis"))
Console.println(nombres.contains("Pedro"))

Trie agenda = Trie()
agenda.insert("Ana")
agenda.insert("Anabel")
agenda.insert("Luis")
Console.println(agenda.searchPrefix("Ana"))
```

Salida:

```
1
false
[Ana, Anabel]
```

> Las secciones 3 a 7 (recursión, matrices, cadenas, matemáticas e integrador)
> continúan en [07-algoritmos-avanzado.md](07-algoritmos-avanzado.md).