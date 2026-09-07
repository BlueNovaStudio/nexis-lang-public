# 🏷️ Clases y objetos en Nexis

Una `class` combina **datos (campos)** y **comportamiento (métodos)**. Es la base para crear objetos y, en particular, **tipos de error propios** que heredan de `Error`.

## 1. Sintaxis

```nexis
class NombreClase {
    // campos (variables)
    tipo campo = valor_inicial

    // métodos (funciones)
    tipo metodo(parametros) -> retorno {
        // cuerpo
    }
}
```

## 2. Ejemplo: una cuenta bancaria

```nexis
class Cuenta {
    float saldo = 0

    void depositar(float: monto) {
        saldo = saldo + monto
    }

    void retirar(float: monto) {
        if monto <= saldo {
            saldo = saldo - monto
        } else {
            Console.print("Saldo insuficiente")
        }
    }

    float consultar() -> float {
        saldo
    }
}
```

**Uso:**

```nexis
Cuenta miCuenta = Cuenta()
miCuenta.depositar(500)
miCuenta.depositar(150)
miCuenta.retirar(200)

float total = miCuenta.consultar()   // 450
Console.print("Saldo: " + total)
```

Los métodos se llaman con el operador punto (`.`). Dentro de la clase, los métodos acceden a los campos por su nombre directamente.

## 3. El tipo `Error` y los errores propios

El sistema de manejo de errores está basado en la clase `Error`. Puedes **definir tus propios errores** heredando de `Error` para lanzar excepciones con significado:

```nexis
class ErrorSaldoInsuficiente : Error {
    // hereda mensaje(), codigo(), etc. de Error
}

void transferir(float: monto, float: saldo) {
    if monto > saldo {
        lanzar ErrorSaldoInsuficiente("No hay saldo suficiente para transferir")
    }
    Console.print("Transferencia realizada")
}

try {
    transferir(1000, 200)
} catch (ErrorSaldoInsuficiente e) {
    Console.print("Rechazado: " + e.mensaje())
}
```

> El `catch` evalúa los tipos de error del más específico al más general, igual que con los errores nativos. Consulta [try_catch](../errors/try_catch.md).

## 4. Buenas prácticas

1. **Una clase = una responsabilidad.** No mezcles lógica no relacionada.
2. Nombre las clases en singular con mayúscula inicial: `Cuenta`, `Contacto`, `Usuario`.
3. **Inicializa siempre los campos** para evitar NX00.
4. Usa `struct` si solo agrupas datos; usa `class` cuando necesitas métodos.
5. Para errores propios, hereda de `Error` y lanza siempre con `ErrorTipo("mensaje")` (ver NX43).