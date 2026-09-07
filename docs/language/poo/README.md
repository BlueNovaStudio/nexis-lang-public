# 🏛️ Programación orientada a objetos (POO) en Nexis

La programación orientada a objetos permite agrupar **datos** y **comportamiento** en entidades reutilizables. Nexis soporta `struct` para agrupar datos y `class` para definir tipos de objetos con métodos.

> En la versión demo v0.0.1, el soporte de POO está pensado especialmente para los **tipos de error** (`Error` y sus subclases) y para estructuras de datos con varios campos (por ejemplo, los contactos de una agenda).

## Contenido

- [Structs (agrupación de datos)](structs.md)
- [Clases y objetos](classes.md)

## En esta sección aprenderás

- Definir un `struct` con varios campos.
- Definir una `class` con métodos.
- Crear y usar objetos.
- Crear tipos de error propios heredando de `Error`.

## Referencia rápida

```nexis
// struct: agrupa datos
struct Contacto {
    string nombre
    string telefono
    string categoria
}

// class: datos + métodos
class Cuenta {
    float saldo = 0

    void depositar(float: monto) {
        saldo = saldo + monto
    }

    float consultar() -> float {
        saldo
    }
}

// Uso
Contacto c = Contacto()
c.nombre = "Ana"
c.telefono = "123456"

Cuenta miCuenta = Cuenta()
miCuenta.depositar(500)
float total = miCuenta.consultar()
```