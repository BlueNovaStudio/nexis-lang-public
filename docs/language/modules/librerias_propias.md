# 📚 Crear librerías propias en Nexis

## Introducción

Un archivo `.nex` se convierte en una **librería propia** cuando otro archivo lo importa con `#inject`. La librería es un módulo normal de Nexis: define funciones, estructuras y clases que quedan disponibles para quien la importe. No hace falta declarar "exportados" ni una sintaxis especial: **todo lo definido en el archivo es lo que se expone**.

---

## 1. Qué puede contener una librería

Un módulo propio es un archivo con extensión `.nex` que puede declarar:

- **Funciones** con retorno: `func nombre(...) -> tipo { ... }`.
- **Procedimientos** sin retorno: `void nombre(...) { ... }`.
- **Constantes** globales: `const tipo NOMBRE = valor`.
- **Estructuras** y **clases**: `struct`/`class` (ver POO).
- Sus propias **importaciones** con `#inject` (librerías nativas u otros módulos propios).

Ejemplo de una librería `geometria.nex`:

```
#/ geometria.nex — módulo de funciones geométricas.

#inject math;

const double PI2 = 6.283185307

func areaCirculo(float: radio) -> float {
    emit -> math.PI * radio * radio
}

func perimetroCirculo(float: radio) -> float {
    emit -> 2 * math.PI * radio
}

class Punto {
    float x = 0
    float y = 0

    void mover(float: nuevo_x, float: nuevo_y) {
        x = nuevo_x
        y = nuevo_y
    }
}
```

---

## 2. Cómo se usa una librería propia

### 2.1 Importar con `#inject`

La importación se hace al inicio del archivo que consume la librería:

```
#inject "geometria.nex";
```

### 2.2 Llamar a sus símbolos

Las funciones, clases y constantes de la librería se usan **sin prefijo**, directamente por su nombre:

```
#inject "geometria.nex";

Console.print(areaCirculo(5.0))     // ≈ 78.54

Punto p = Punto()
p.mover(3.0, 4.0)
```

### 2.3 Rutas

- **Relativas** al archivo que importa: `#inject "utilidades/calculos.nex";`.
- **Absolutas** con la ruta completa.
- La extensión **debe ser `.nex`** (error [NX83](../errors/catalog-04-io-modulos-y-sistema.md#nx83-extensión-de-archivo-inválida-en-inject)).

---

## 3. Propagación de importaciones

Una librería **importa lo que necesita para funcionar**, y esas importaciones se resuelven dentro del propio módulo. Si `superficies.nex` importa `math`, sus funciones pueden usar `math.PI` sin que el programa principal tenga que importar `math`:

```
#/ superficies.nex
#inject math;

func circunferencia(float: radio) -> float {
    emit -> 2 * math.PI * radio
}
```

```
#/ app.nxs
#inject "superficies.nex";

Console.print(circunferencia(5.0))   // funciona: el módulo importa math
```

### Regla de propagación

1. Las importaciones de un módulo están disponibles **dentro de ese módulo**.
2. Los símbolos **definidos** en un módulo (funciones, clases, constantes) quedan disponibles para quien lo importa.
3. Las variables de nivel superior de un módulo son locales al módulo: no "escapan" a quien lo importa.

---

## 4. Errores relacionados con librerías propias

| Código | Situación | Solución |
|--------|-----------|----------|
| [NX80](../errors/catalog-04-io-modulos-y-sistema.md#nx80-módulo-no-encontrado) | La ruta del archivo no existe | Corregir la ruta o crear el archivo |
| [NX81](../errors/catalog-04-io-modulos-y-sistema.md#nx81-importación-circular) | A importa a B y B importa a A | Extraer lo compartido a un módulo común |
| [NX82](../errors/catalog-04-io-modulos-y-sistema.md#nx82-función-usada-sin-importar) | Usar una función de un módulo sin importarlo | Agregar `#inject "modulo.nex";` |
| [NX83](../errors/catalog-04-io-modulos-y-sistema.md#nx83-extensión-de-archivo-inválida-en-inject) | El archivo no tiene extensión `.nex` | Renombrar a `.nex` |
| [NX84](../errors/catalog-04-io-modulos-y-sistema.md#nx84-símbolo-no-encontrado-en-el-módulo-importado) | Llamar un símbolo que el módulo no define | Corregir el nombre o importar el módulo correcto |

### Importaciones circulares (NX81)

Dos (o más) módulos no pueden importarse entre sí. Si `a.nex` importa `b.nex` y `b.nex` importa `a.nex`, Nexis no puede ordenar las dependencias y reporta NX81. La solución es extraer los símbolos compartidos a un tercer módulo `comun.nex` que ambos importen:

```
#/ a.nex     #inject "comun.nex";
#/ b.nex     #inject "comun.nex";
#/ comun.nex define lo que a y b comparten
```

---

## 5. Ejemplo completo

### `operaciones.nex`

```
#/ operaciones.nex — librería de operaciones con cadenas.
#inject string;

func repetir(string: texto, int: veces) -> string {
    string resultado = ""
    for i in 0 .. veces {
        resultado = resultado + texto
    }
    emit -> resultado
}

func iniciar_mayuscula(string: texto) -> string {
    emit -> string.uppercase(string.subcadena(texto, 0, 1)) +
           string.subcadena(texto, 1, string.length(texto))
}
```

### `app.nxs`

```
#inject "operaciones.nex";

string saludo = repetir("ja", 3)
Console.println(saludo)                  // jajaja
Console.println(iniciar_mayuscula("hola"))   // Hola
```

---

## 6. Buenas prácticas

1. **Un archivo, una responsabilidad:** separa cálculos, estructuras y utilidades en módulos distintos.
2. **Nombres descriptivos:** `operaciones_aritmeticas.nex`, no `ops.nex`.
3. **`#inject` al inicio:** coloca todas las importaciones al principio del archivo (regla general de todo programa Nexis).
4. **Evita ciclos:** diseña dependencias en una sola dirección; usa un módulo "base" común para romper ciclos.
5. **Documenta qué expone el módulo:** un comentario `#/` con el propósito y sus funciones ayuda a quien la use.
6. **Solo importa lo que usas:** cada `#inject` adicional consume memoria y puede crear ambigüedades ([NX82](../errors/catalog-04-io-modulos-y-sistema.md#nx82-función-usada-sin-importar)).

---

## Contenido relacionado

- [Módulos e importación](imports.md) - visión general de `#inject`.
- [Importación de librerías](imports.md) — sintaxis de `#inject` y librerías nativas.
- [POO: clases](../poo/classes.md) — clases y herencia dentro de un módulo.
- [Catálogo de errores NX](../errors/errors.md) — NX80, NX81, NX82, NX83, NX84.
