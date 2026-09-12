# 💻 Ejemplos de Nexis

Programas de ejemplo listos para probar, organizados en orden de dificultad. Cada ejemplo sigue la documentación oficial y usa solo construcciones validadas por los tests del lenguaje.

## Ejemplos

| # | Archivo | Qué muestra |
|---|---------|-------------|
| 0 | [hola_mundo.nxs](00_hola_mundo.nxs) | Impresión por consola (`Console.print` / `Console.println`). |
| 1 | [variables_y_tipos.nxs](01_variables_y_tipos.nxs) | Tipos primitivos, `const` e inferencia de tipos. |
| 2 | [operadores.nxs](02_operadores.nxs) | Entrada por teclado y operadores aritméticos, relacionales y lógicos. |
| 3 | [control_de_flujo.nxs](03_control_de_flujo.nxs) | `if/else if/else` y `switch` con casos agrupados. |
| 4 | [bucles.nxs](04_bucles.nxs) | `for`, `break`, recursión y `#inject math`. |
| 5 | [funciones.nxs](05_funciones.nxs) | Funciones con retorno (`emit ->`), `void` y composición. |
| 6 | [manejo_de_errores.nxs](06_manejo_de_errores.nxs) | `try/catch/finally` y `lanzar` errores personalizados. |
| 7 | [estructuras_de_datos.nxs](07_estructuras_de_datos.nxs) | `Vector`, `Map` y `Set`. |
| 8 | [librerias_estandar.nxs](08_librerias_estandar.nxs) | Librerías `math`, `string` y `random`. |
| 9 | [módulos](modulos/01_usar_modulo.nxs) | Importación de módulos propios con `#inject "archivo.nex"`. |

## Cómo ejecutarlos

El intérprete (`nexisi`) y el compilador (`nexisc`) ya están disponibles en la **demo v0.0.1**:

```bash
nexisi archivo.nxs     # o: nexisc archivo.nxs
```

> La implementación actual (v0.0.1) es una **demo**: solo admite los programas de su alcance (tipos, operadores, `Console` e interpolación `fs"…"`). Los ejemplos avanzados (control de flujo, funciones, errores, POO y módulos) forman parte del alcance de la documentación y de la suite de tests; su ejecución llegará con **Nexis V1.0.0**. Mientras tanto sirven como referencia de sintaxis.

## Convenciones de los ejemplos

- Los comentarios de bloque se escriben con `#/ ...`.
- Los ficheros de módulos usan la extensión `.nex`; los programas principales usan `.nxs`.
- Los ejemplos de entrada (`Console.input`) son interactivos: piden datos por teclado.