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

Cuando el intérprete esté disponible (pendiente de **Nexis V1.0.0**), ejecuta:

```bash
nexis archivo.nxs
```

Mientras tanto, los archivos sirven como referencia de sintaxis y son los mismos que usa la suite de tests del lenguaje.

## Convenciones de los ejemplos

- Los comentarios de bloque se escriben con `#/ ...`.
- Los ficheros de módulos usan la extensión `.nex`; los programas principales usan `.nxs`.
- Los ejemplos de entrada (`Console.input`) son interactivos: piden datos por teclado.