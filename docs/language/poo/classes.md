# 🏷️ Clases y objetos en Nexis

Una `class` combina **datos (campos)** y **comportamiento (métodos)**. En la versión actual puedes crear objetos con `NombreClase()`, modificar campos y llamar sus métodos.

## 1. Sintaxis

```nexis
class NombreClase {
    // campos sin inicializador terminan en ';'
    // los campos inicializados no llevan ';'
    tipo campo;
    tipo campo_con_valor = valor_inicial

    init(self, tipo: parametro) {
        self.campo = parametro
    }

    // métodos (funciones)
    func metodo(parametros) -> retorno {
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

    func consultar() -> float {
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

## 3. Una clase que encapsula un vector

Las clases pueden agrupar una colección nativa y exponer sus operaciones como métodos propios. Así puedes usar exactamente `nums.add(3)` y `nums.remove(indice)` sobre una instancia de tu clase:

```nexis
#inject Vector;

class VectorPropio {
    Vector<int> datos = []
    int cantidad = 0

    void add(int: valor) {
        datos.add(valor)
        cantidad = cantidad + 1
    }

    void remove(int: indice) {
        datos.remove(indice)
        cantidad = cantidad - 1
    }

    func get(int: indice) -> int {
        datos.get(indice)
    }

    func length() -> int {
        cantidad
    }
}

VectorPropio nums = VectorPropio()
nums.add(1)
nums.add(4)
nums.add(2)
nums.remove(1)
Console.println(nums.get(1))   // 2
Console.println(nums.length()) // 2
```

`remove(indice)` usa índices desde cero y produce el error de índice fuera de rango si el índice no existe. `#inject Vector;` debe aparecer antes de usar `Vector<T>`.

## 4. Constructor `init`

Una clase puede definir un único método especial `init`. El objeto se crea con `NombreClase(argumentos)` y Nexis ejecuta `init` automáticamente. `self` es la instancia que se está construyendo; se escribe sin tipo y no cuenta como argumento del constructor.

```nexis
class Punto {
    int x = 0
    int y = 0

    init(self, int: horizontal, int: vertical) {
        self.x = horizontal
        self.y = vertical
    }

    func suma() -> int {
        x + y
    }
}

Punto p = Punto(4, 7)
Console.println(p.suma()) // 11
```

El constructor no declara tipo de retorno. Si una clase define `init`, la cantidad de argumentos de `NombreClase(...)` debe coincidir con sus parámetros excepto `self`. Si no define `init`, se conserva el constructor por defecto existente.

## 5. Alcance actual

Las clases admiten campos con valores iniciales literales o por defecto del tipo, constructor `init`, métodos `void` y métodos `func` con retorno. Los métodos pueden leer y modificar campos directamente por su nombre o mediante `self.campo`, y llamar métodos de sus campos, incluidas las colecciones. Todos los campos y métodos son públicos. Herencia y modificadores de acceso aún no están implementados. Para errores, usa los tipos incorporados descritos en [try_catch](../errors/try_catch.md).

## 6. Buenas prácticas

1. **Una clase = una responsabilidad.** No mezcles lógica no relacionada.
2. Nombre las clases en singular con mayúscula inicial: `Cuenta`, `Contacto`, `Usuario`.
3. **Inicializa siempre los campos** para evitar NX00.
4. Usa `struct` si solo agrupas datos; usa `class` cuando necesitas métodos.
5. Usa `#inject Vector;` (o la estructura correspondiente) antes de emplear una colección en los campos de la clase.
