# Librería Map en Nexis

`Map<K, V>` almacena parejas **clave → valor**. Cada clave aparece una
sola vez; asignar de nuevo la misma clave actualiza su valor.

## 1. Importación

```
#inject Map;
```

## 2. Declaración e inicialización

```
Map<string, int> vacio = {}
Map<string, int> inventario = {"manzanas": 50, "peras": 30}
Map<int, string> nombres = {1: "Ana", 2: "Luis"}
```

Las llaves **con `:`** representan un mapa; las llaves **sin `:`**
representan un conjunto (`Set`).

## 3. Métodos

| Método | Parámetros | Devuelve | Descripción |
|--------|------------|----------|-------------|
| `put(clave, valor)` / `set` / `poner` | `K`, `V` | `void` | Crea o actualiza la pareja. |
| `get(clave)` / `obtener` | `K` | `V` | Devuelve el valor; `NX52` si no existe. |
| `contains(clave)` / `contiene` | `K` | `bool` | Comprueba si la clave existe. |
| `remove(clave)` / `eliminar` | `K` | `void` | Elimina la pareja si existe. |
| `keys()` / `claves` | — | `Vector<K>` | Vector con las claves. |
| `values()` / `valores` | — | `Vector<V>` | Vector con los valores. |
| `length()` / `longitud` | — | `int` | Número de parejas. |
| `isEmpty()` / `esta_vacio` | — | `bool` | `true` si está vacío. |

> `get` lanza `NX52` si la clave no existe. Comprueba antes con
> `contains` si no estás seguro.

## 4. Ejemplo: frecuencia de palabras

```
#inject Map;
#inject Vector;
#inject string;

string frase = "el gato y el perro y el gato"
Vector<string> palabras = string.dividir(frase, " ")
Map<string, int> frecuencia = {}

foreach (palabra in palabras) {
    if (frecuencia.contains(palabra)) {
        frecuencia.put(palabra, frecuencia.get(palabra) + 1)
    } else {
        frecuencia.put(palabra, 1)
    }
}

foreach (clave in frecuencia) {
    Console.println(clave + ": " + frecuencia.get(clave))
}
// el: 3
// gato: 2
// y: 2
// perro: 1
```

## 5. Recorrido

`foreach` sobre un `Map` entrega las **claves**:

```
Map<string, int> edades = {"Ana": 20, "Luis": 25}

foreach (nombre in edades) {
    Console.println(nombre + " -> " + edades.get(nombre))
}

foreach (clave in edades.keys()) {
    Console.println(clave)
}

foreach (valor in edades.values()) {
    Console.println(valor)
}
```

## 6. Ejemplo: agenda telefónica

```
#inject Map;

Map<string, string> agenda = {}
agenda.put("Ana", "111")
agenda.put("Luis", "222")
agenda.put("Ana", "333")      // actualiza, no duplica

Console.println(agenda.length())          // 2
Console.println(agenda.get("Ana"))        // 333
Console.println(agenda.contains("Eva"))   // false

agenda.remove("Luis")
Console.println(agenda.length())          // 1
```

## 7. Errores comunes

| Error | Código | Solución |
|-------|--------|----------|
| Leer clave inexistente | `NX52` | Usar `contains` antes de `get`. |
| Mezclar tipos de clave | `NX07` | Un solo tipo de clave y de valor. |
| Confundir `{}` con conjunto | — | Usar `{"clave": valor}` para mapas. |

## 8. Complejidad

`put`, `get`, `contains` y `remove` son O(1) promedio. `keys` y `values`
son O(n).
