# Librería String en Nexis

La librería `string` permite consultar, transformar y dividir cadenas de
texto.

## 1. Importación

```
#inject string;
```

## 2. Funciones implementadas

| Función | Parámetros | Devuelve | Descripción |
|---------|------------|----------|-------------|
| `length(texto)` / `longitud` | `string` | `int` | Número de caracteres. |
| `lowercase(texto)` / `minusculas` | `string` | `string` | Convierte a minúsculas. |
| `uppercase(texto)` / `mayusculas` | `string` | `string` | Convierte a mayúsculas. |
| `trim(texto)` / `recortar` | `string` | `string` | Quita espacios de los extremos. |
| `split(texto, separador)` / `dividir` | `string`, `string` | `Vector<string>` | Divide por separador. |
| `contains(texto, fragmento)` / `contiene` | `string`, `string` | `bool` | Comprueba si contiene. |
| `startsWith(texto, prefijo)` / `comienza_con` | `string`, `string` | `bool` | Comprueba el prefijo. |

### Detalles de los parámetros

- `texto` y `separador` deben ser `string`. Otros tipos se convierten a
  texto cuando es posible.
- `split(texto, "")` devuelve un vector con **cada carácter** como
  elemento.
- `length` cuenta caracteres Unicode, no bytes.
- Los alias en español funcionan exactamente igual que los ingleses.

## 3. Ejemplo completo

```
#inject string;
#inject Vector;

string nombre = "  Nexis  "
string limpio = string.trim(nombre)
string titulo = string.uppercase(limpio)

Console.println(limpio)                       // Nexis
Console.println(titulo)                       // NEXIS
Console.println(string.length(limpio))        // 5
Console.println(string.contains(limpio, "ex")) // true
Console.println(string.startsWith(limpio, "Ne")) // true

Vector<string> palabras = string.split("uno,dos,tres", ",")
foreach (p in palabras) {
    Console.println(p)
}
// uno
// dos
// tres
```

## 4. Ejemplo: separar por caracteres

```
#inject string;
#inject Vector;

Vector<string> letras = string.split("Nexis", "")
Console.println(letras.length())   // 5
foreach (letra in letras) {
    Console.println(letra)
}
```

## 5. Concatenación y comparación

Nexis permite concatenar con `+` y comparar con `==`, `!=`, `<`, `>`:

```
string a = "Hola"
string b = " Mundo"
string c = a + b
Console.println(c)          // Hola Mundo
Console.println(a == "Hola") // true
Console.println(a < b)       // false (orden lexicográfico)
```

## 6. Funciones reservadas (no disponibles en V0.0.6)

Estas funciones aparecen en la API planificada, pero **todavía no están
implementadas**:

- `endsWith` / `termina_con`
- `replace` / `reemplazar`
- `substring` / `subcadena`
- `indexOf` / `indice_de`
- `join` / `unir`
- `toInt`, `toFloat`, `toDouble`

Para convertir texto a número usa la función de conversión del lenguaje:

```
int n = int("42")
float f = float("3.14")
```

## 7. Errores comunes

| Error | Solución |
|-------|----------|
| Llamar `endsWith` en V0.0.6 | No está implementada; usar `contains` o comparar manualmente. |
| `split` con separador inexistente | Devuelve un vector con el texto completo. |
| Índice de string fuera de rango | Usar `0 ... string.length(texto)`. |
