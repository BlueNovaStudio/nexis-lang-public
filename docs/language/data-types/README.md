# 🧱 Tipos de datos en Nexis

Nexis es un lenguaje de **tipado estático**: cada variable tiene un tipo fijo que se conoce desde su declaración. Los tipos se dividen en **primitivos** (números, texto, booleano) y **estructuras de datos** (colecciones).

## Contenido

- [Tipos primitivos](primitive-types.md)
- [Estructuras de datos](data-struture.md)

## En esta sección aprenderás

- Los tipos primitivos (enteros, decimales, texto, booleano).
- Las estructuras de datos genéricas (`Vector`, `Stack`, `Map`, etc.).
- Reglas de tipado: inferencia con `auto`, constantes con `const` y conversiones.

## Referencia rápida

```nexis
int entero = 42
float precio = 3.14f
double sueldo = 2500.99
char letra = 'A'
string nombre = "Nexis"
bool activo = true

auto deducido = 10        // auto deduce int
const double PI = 3.14159

Vector<int> numeros = [1, 2, 3]
```

## Flujo recomendado

1. Revisa los tipos primitivos.
2. Practica declarar variables de cada tipo.
3. Avanza a las estructuras de datos.

> Conocer bien los tipos evita los errores NX07, NX10 y NX12. Consulta el [catálogo de errores](../errors/errors.md).