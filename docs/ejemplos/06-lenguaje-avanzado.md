# 🧭 Lenguaje Nexis avanzado: parte 2

Continuación de [01-lenguaje.md](01-lenguaje.md): variables globales, structs,
clases, manejo de errores, módulos, entrada del usuario, comentarios y un
programa integrador que une todo lo anterior.

---

## 8. Variables globales y paso de colecciones

Las funciones ven y modifican las globales. Las colecciones y los structs se
pasan con **copia de salida**: los cambios vuelven al llamador.

```nexis
#inject Vector;

int contador = 0
Vector<int> historial = []

void incrementar() -> void {
    contador = contador + 1
    historial.add(contador)
}

void ordenar(Vector<int>: v) -> void {
    v.sort()
}

incrementar()
incrementar()
incrementar()

Console.println(contador)
Console.println(historial)

Vector<int> datos = [3, 1, 2]
ordenar(datos)
Console.println(datos)
```

Salida:

```
3
[1, 2, 3]
[1, 2, 3]
```

### Shadowing: la local oculta la global

```nexis
int valor = 100

func local() -> int {
    int valor = 5
    emit -> valor
}

Console.println(local())
Console.println(valor)
```

Salida:

```
5
100
```

---

## 9. Structs

Un `struct` agrupa campos con nombre. Se construye con `Nombre(valor1, valor2)`
y los campos se leen con `.campo`.

```nexis
struct Producto {
    string nombre;
    int precio;
    int stock;
}

Producto arroz = Producto("Arroz", 1500, 10)
Console.println(arroz.nombre)
Console.println(arroz.precio)
Console.println(arroz.stock)

arroz.precio = 1700
arroz.stock = arroz.stock - 3
Console.println(arroz.precio + " / " + arroz.stock)
```

Salida:

```
Arroz
1500
10
1700 / 7
```

### Structs dentro de colecciones

```nexis
#inject Vector;

struct Punto {
    int x;
    int y;
}

Vector<Punto> puntos = []
puntos.add(Punto(1, 2))
puntos.add(Punto(3, 4))

int suma_x = 0
foreach (Punto p, puntos) {
    suma_x = suma_x + p.x
}
Console.println("suma x = " + suma_x)
Console.println(puntos[1].y)
```

Salida:

```
suma x = 4
4
```

### Pasar un struct a una función (copia de salida)

```nexis
struct Cuenta {
    int saldo;
}

void depositar(Cuenta: c, int: monto) -> void {
    c.saldo = c.saldo + monto
}

Cuenta mia = Cuenta(100)
depositar(mia, 50)
Console.println(mia.saldo)
```

Salida:

```
150
```

---

## 10. Clases, `init` y `self`

Una clase encapsula estado y métodos. `init` es el constructor; dentro de los
métodos, `self` (o `this`) apunta al objeto y los campos se pueden usar
directamente.

```nexis
class Cuenta {
    float saldo = 0
    int operaciones = 0

    init(self, float: inicial) {
        self.saldo = inicial
    }

    void depositar(float: monto) {
        saldo = saldo + monto
        operaciones = operaciones + 1
    }

    func retirar(float: monto) -> bool {
        if (monto > saldo) {
            emit -> false
        }
        saldo = saldo - monto
        operaciones = operaciones + 1
        emit -> true
    }

    func resumen() -> string {
        emit -> "saldo=" + saldo + " ops=" + operaciones
    }
}

Cuenta c = Cuenta(100.0)
c.depositar(50.0)
bool ok = c.retirar(30.0)
bool no = c.retirar(1000.0)

Console.println(ok)
Console.println(no)
Console.println(c.resumen())
```

Salida:

```
true
false
saldo=120 ops=2
```

### Clase con colección interna

```nexis
#inject Vector;

class Carrito {
    Vector<string> items = []

    void agregar(string: item) {
        items.add(item)
    }

    func total() -> int {
        emit -> items.length()
    }

    func listar() -> void {
        foreach (i in items) {
            Console.println("- " + i)
        }
    }
}

Carrito carrito = Carrito()
carrito.agregar("pan")
carrito.agregar("leche")
carrito.listar()
Console.println("items: " + carrito.total())
```

Salida:

```
- pan
- leche
items: 2
```

---

## 11. Manejo de errores

```nexis
try {
    int resultado = 10 / 0
    Console.println(resultado)
} catch (ErrorDivision e) {
    Console.println("No se puede dividir entre cero")
}

#inject Vector;

Vector<int> datos = [10, 20, 30]
try {
    Console.println(datos.get(8))
} catch (ErrorIndice e) {
    Console.println("Índice fuera de rango")
}
```

Salida:

```
No se puede dividir entre cero
Índice fuera de rango
```

### `finally` y errores personalizados

```nexis
func validar_edad(int: edad) -> void {
    if (edad < 0) {
        lanzar ErrorValidacion("La edad no puede ser negativa")
    }
    if (edad < 18) {
        lanzar ErrorValidacion("Menor de edad no permitido")
    }
    Console.println("Edad válida")
}

try {
    validar_edad(-5)
} catch (ErrorValidacion e) {
    Console.println("Rechazado: " + e.mensaje())
} finally {
    Console.println("Fin de la validación")
}
```

Salida:

```
Rechazado: La edad no puede ser negativa
Fin de la validación
```

### Varios `catch` y relanzar

```nexis
func nivel_interno() -> void {
    lanzar ErrorIndice("fallo interno")
}

try {
    try {
        nivel_interno()
    } catch (Error e) {
        Console.println("Interno capturado")
        lanzar e
    }
} catch (Error e) {
    Console.println("Externo: " + e.mensaje())
}
```

Salida:

```
Interno capturado
Externo: fallo interno
```

---

## 12. Módulos

### Librerías nativas

```nexis
#inject math;
#inject string;

Console.println(math.sqrt(81))
Console.println(string.uppercase("nexis"))
```

Salida:

```
9
NEXIS
```

### Archivos propios (`.nex`)

Un módulo propio es un archivo `.nex` con funciones, structs o clases. Se
importa con la ruta entre comillas:

```
# geometria.nex
#inject math;

func area_circulo(float: r) -> float {
    emit -> math.PI * r * r
}

func perimetro_circulo(float: r) -> float {
    emit -> 2 * math.PI * r
}
```

```
# main.nxs
#inject "geometria.nex";

Console.println(area_circulo(5.0))
Console.println(perimetro_circulo(5.0))
```

Salida:

```
78.53981633974483
31.41592653589793
```

> Este ejemplo necesita dos archivos, así que no se ejecuta en esta página.
> La versión funcional está en `compiler/examples/07_modulos/` y la suite la
> ejecuta en cada pasada.

---

## 13. Entrada del usuario

`Console.input()` lee una línea y la convierte al tipo de la variable. Admite
un texto de ayuda con `text=`.

```nexis
// doc: input Ana|25
string nombre = Console.input(text="Nombre: ")
int edad = Console.input(text="Edad: ")

Console.println("Hola " + nombre)
Console.println("El año que viene tendrás " + (edad + 1))
```

Salida:

```
Nombre: Edad: Hola Ana
El año que viene tendrás 26
```

---

## 14. Comentarios

```nexis
# Comentario de línea con numeral
// Comentario de línea con barras

/*
   Comentario
   de bloque
*/

Console.println("Los comentarios no afectan la salida")   // al final de línea
```

Salida:

```
Los comentarios no afectan la salida
```

---

## 15. Programa integrador

Une tipos, funciones, plantillas, structs, colecciones y errores:

```nexis
#inject Vector;

struct Producto {
    string nombre;
    int precio;
    int stock;
}

Vector<Producto> inventario = []

void agregar(Producto: p) -> void {
    inventario.add(p)
}

template <type_full T>
func contiene(Vector<T>: lista, T: objetivo) -> bool {
    foreach (item in lista) {
        if (item == objetivo) {
            emit -> true
        }
    }
    emit -> false
}

func valor_total() -> int {
    int total = 0
    foreach (Producto p, inventario) {
        total = total + p.precio * p.stock
    }
    emit -> total
}

func buscar(string: nombre) -> Producto {
    foreach (Producto p, inventario) {
        if (p.nombre == nombre) {
            emit -> p
        }
    }
    lanzar ErrorValidacion("No existe el producto " + nombre)
}

agregar(Producto("Arroz", 1500, 10))
agregar(Producto("Leche", 3200, 5))
agregar(Producto("Pan", 800, 20))

Console.println("Valor del inventario: " + valor_total())
Console.println("Productos: " + inventario.length())

try {
    Producto p = buscar("Leche")
    Console.println(p.nombre + " cuesta " + p.precio)
} catch (ErrorValidacion e) {
    Console.println(e.mensaje())
}

try {
    buscar("Café")
} catch (ErrorValidacion e) {
    Console.println("Error esperado: " + e.mensaje())
}
```

Salida:

```
Valor del inventario: 47000
Productos: 3
Leche cuesta 3200
Error esperado: No existe el producto Café
```