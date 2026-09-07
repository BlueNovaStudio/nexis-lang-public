# 📇 Structs en Nexis

Un `struct` agrupa varios campos de datos bajo un solo tipo. Es la forma de crear **registros** con varios campos, como un contacto, un punto en el plano o un producto.

## 1. Sintaxis

El `struct` se define con la palabra clave `struct` seguida del nombre y un bloque con los campos:

```nexis
struct Contacto {
    string nombre
    string telefono
    string categoria
}
```

Cada campo se declara como una variable: `tipo nombre`. No se asignan valores en la definición.

## 2. Crear y usar un struct

```nexis
Contacto persona = Contacto()
persona.nombre = "Ana"
persona.telefono = "123456789"
persona.categoria = "trabajo"

Console.print(persona.nombre)   // Ana
```

Los campos se acceden con el operador punto (`.`).

## 3. Ejemplo completo

```nexis
struct Punto {
    int x
    int y
}

Punto origen = Punto()
origen.x = 0
origen.y = 0

Punto destino = Punto()
destino.x = 10
destino.y = 5

int dx = destino.x - origen.x
int dy = destino.y - origen.y
Console.print("Desplazamiento: (" + dx + ", " + dy + ")")
```

## 4. Structs dentro de colecciones

Los structs se pueden almacenar en vectores y mapas:

```nexis
#inject vector;

struct Contacto {
    string nombre
    string telefono
}

Vector<Contacto> agenda = []

Contacto c = Contacto()
c.nombre = "Luis"
c.telefono = "987654321"
agenda.agregar(c)

Console.print(agenda.obtener(0).nombre)   // Luis
```

## 5. Buenas prácticas

1. **Nombra los structs en singular** con mayúscula inicial: `Contacto`, `Punto`, `Producto`.
2. Usa campos descriptivos con `snake_case`.
3. Usa `struct` cuando solo necesites agrupar datos (sin comportamiento). Si necesitas métodos, usa `class` (ver [classes.md](classes.md)).
4. Cuando un campo puede tener valores no válidos, valídalos antes de asignarlos para evitar errores NX07.