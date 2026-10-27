# 🧩 Catálogo de errores de Nexis (códigos NX)

Este documento es la **referencia oficial de errores** de Nexis. Cada error tiene un código único con el formato `NXXX` para que sea fácil de buscar, reportar y resolver.

> **Cómo usar este catálogo:** busca el código `NXxx` en tu mensaje de error, ve a la sección correspondiente y sigue la solución paso a paso. Si el código no aparece en la tabla, revisa las [categorías del catálogo](#categorías-del-catálogo).

## Navegación rápida

- [Manejo de excepciones (try/catch)](try_catch.md)
- [Documentación principal](../../README.md)
- [Guía rápida de errores](../../errores.md)

---

## Tabla de códigos

| Código | Error | Categoría |
|--------|-------|-----------|
| [NX00](catalog-01-variables-y-tipos.md#nx00-variable-no-inicializada) | Variable no inicializada | Variables |
| [NX01](catalog-01-variables-y-tipos.md#nx01-división-por-cero) | División por cero | Variables |
| [NX02](catalog-01-variables-y-tipos.md#nx02-variable-no-definida) | Variable no definida | Variables |
| [NX03](catalog-01-variables-y-tipos.md#nx03-reasignación-de-constante) | Reasignación de constante | Variables |
| [NX04](catalog-01-variables-y-tipos.md#nx04-declaración-duplicada) | Declaración duplicada | Variables |
| [NX05](catalog-01-variables-y-tipos.md#nx05-identificador-inválido) | Identificador inválido | Variables |
| [NX06](catalog-01-variables-y-tipos.md#nx06-constante-sin-inicializar) | Constante sin inicializar | Variables |
| [NX07](catalog-01-variables-y-tipos.md#nx07-tipo-incompatible-en-asignación) | Tipo incompatible en asignación | Variables |
| [NX08](catalog-01-variables-y-tipos.md#nx08-variable-auto-sin-inicializador) | Variable `auto` sin inicializador | Variables |
| [NX09](catalog-01-variables-y-tipos.md#nx09-valor-fuera-del-rango-del-tipo) | Valor fuera del rango del tipo | Variables |
| [NX10](catalog-01-variables-y-tipos.md#nx10-operandos-con-tipos-incompatibles) | Operandos incompatibles | Tipos |
| [NX11](catalog-01-variables-y-tipos.md#nx11-índice-fuera-de-rango) | Índice fuera de rango | Tipos |
| [NX12](catalog-01-variables-y-tipos.md#nx12-conversión-de-tipo-inválida) | Conversión de tipo inválida | Tipos |
| [NX13](catalog-01-variables-y-tipos.md#nx13-operación-matemática-inválida) | Operación matemática inválida | Tipos |
| [NX14](catalog-01-variables-y-tipos.md#nx14-tipo-de-retorno-incompatible) | Tipo de retorno incompatible | Tipos |
| [NX15](catalog-01-variables-y-tipos.md#nx15-tipo-no-reconocido) | Tipo no reconocido | Tipos |
| [NX16](catalog-01-variables-y-tipos.md#nx16-carácter-inválido) | Carácter inválido | Tipos |
| [NX17](catalog-01-variables-y-tipos.md#nx17-índice-o-clave-de-tipo-inválido) | Índice o clave de tipo inválido | Tipos |
| [NX18](catalog-01-variables-y-tipos.md#nx18-comparación-entre-tipos-incompatibles) | Comparación entre tipos incompatibles | Tipos |
| [NX19](catalog-01-variables-y-tipos.md#nx19-desbordamiento-aritmético-en-ejecución) | Desbordamiento aritmético en ejecución | Tipos |
| [NX20](catalog-02-control-y-funciones.md#nx20-break-fuera-de-un-bucle) | `break` fuera de un bucle | Control de flujo |
| [NX21](catalog-02-control-y-funciones.md#nx21-continue-fuera-de-un-bucle) | `continue` fuera de un bucle | Control de flujo |
| [NX22](catalog-02-control-y-funciones.md#nx22-paso-de-bucle-inválido) | Paso de bucle inválido | Control de flujo |
| [NX23](catalog-02-control-y-funciones.md#nx23-condición-no-booleana) | Condición no booleana | Control de flujo |
| [NX24](catalog-02-control-y-funciones.md#nx24-caso-duplicado-en-switch) | Caso duplicado en `switch` | Control de flujo |
| [NX25](catalog-02-control-y-funciones.md#nx25-case-o-default-fuera-de-switch) | `case` o `default` fuera de `switch` | Control de flujo |
| [NX26](catalog-02-control-y-funciones.md#nx26-default-duplicado-en-switch) | `default` duplicado en `switch` | Control de flujo |
| [NX27](catalog-02-control-y-funciones.md#nx27-rango-de-case-invertido) | Rango de `case` invertido | Control de flujo |
| [NX28](catalog-02-control-y-funciones.md#nx28-valor-de-case-con-tipo-distinto-al-del-switch) | `case` con tipo distinto al del `switch` | Control de flujo |
| [NX29](catalog-02-control-y-funciones.md#nx29-límites-o-paso-del-for-no-numéricos) | Límites o paso del `for` no numéricos | Control de flujo |
| [NX30](catalog-02-control-y-funciones.md#nx30-ruta-sin-retorno-en-función) | Ruta sin retorno en función | Funciones |
| [NX31](catalog-02-control-y-funciones.md#nx31-falta-tipo-de-retorno) | Falta tipo de retorno | Funciones |
| [NX32](catalog-02-control-y-funciones.md#nx32-cantidad-de-argumentos-incorrecta) | Cantidad de argumentos incorrecta | Funciones |
| [NX33](catalog-02-control-y-funciones.md#nx33-tipo-de-argumento-incorrecto) | Tipo de argumento incorrecto | Funciones |
| [NX34](catalog-02-control-y-funciones.md#nx34-función-declarada-dos-veces) | Función declarada dos veces | Funciones |
| [NX35](catalog-02-control-y-funciones.md#nx35-parámetro-repetido-en-la-firma) | Parámetro repetido en la firma | Funciones |
| [NX36](catalog-02-control-y-funciones.md#nx36-emit-en-función-void) | `emit` en función `void` | Funciones |
| [NX37](catalog-02-control-y-funciones.md#nx37-emit-fuera-de-una-función) | `emit` fuera de una función | Funciones |
| [NX40](catalog-03-errores-y-colecciones.md#nx40-catch-sin-try-previo) | `catch` sin `try` previo | Errores |
| [NX41](catalog-03-errores-y-colecciones.md#nx41-try-vacío) | `try` vacío | Errores |
| [NX42](catalog-03-errores-y-colecciones.md#nx42-error-no-capturado) | Error no capturado | Errores |
| [NX43](catalog-03-errores-y-colecciones.md#nx43-lanzar-un-valor-que-no-es-error) | Lanzar un valor que no es `Error` | Errores |
| [NX44](catalog-03-errores-y-colecciones.md#nx44-aserción-fallida) | Aserción fallida | Errores |
| [NX45](catalog-03-errores-y-colecciones.md#nx45-catch-con-tipo-que-no-es-error) | `catch` con tipo que no es `Error` | Errores |
| [NX46](catalog-03-errores-y-colecciones.md#nx46-catch-sin-variable) | `catch` sin variable | Errores |
| [NX50](catalog-03-errores-y-colecciones.md#nx50-operación-sobre-colección-vacía) | Operación sobre colección vacía | Colecciones |
| [NX51](catalog-03-errores-y-colecciones.md#nx51-modificar-colección-durante-iteración) | Modificar colección durante iteración | Colecciones |
| [NX52](catalog-03-errores-y-colecciones.md#nx52-clave-no-encontrada-en-map) | Clave no encontrada en `Map` | Colecciones |
| [NX53](catalog-03-errores-y-colecciones.md#nx53-operación-no-soportada-por-la-colección) | Operación no soportada por la colección | Colecciones |
| [NX60](catalog-04-io-modulos-y-sistema.md#nx60-formato-de-entrada-inválido) | Formato de entrada inválido | Entrada/Salida |
| [NX61](catalog-04-io-modulos-y-sistema.md#nx61-archivo-no-encontrado) | Archivo no encontrado | Entrada/Salida |
| [NX62](catalog-04-io-modulos-y-sistema.md#nx62-error-de-lecturaescritura) | Error de lectura/escritura | Entrada/Salida |
| [NX63](catalog-04-io-modulos-y-sistema.md#nx63-directorio-no-encontrado-al-listar) | Directorio no encontrado al listar | Entrada/Salida |
| [NX70](catalog-04-io-modulos-y-sistema.md#nx70-error-de-red) | Error de red | Red |
| [NX71](catalog-04-io-modulos-y-sistema.md#nx71-error-gráfico) | Error gráfico | Gráficos |
| [NX80](catalog-04-io-modulos-y-sistema.md#nx80-módulo-no-encontrado) | Módulo no encontrado | Módulos |
| [NX81](catalog-04-io-modulos-y-sistema.md#nx81-importación-circular) | Importación circular | Módulos |
| [NX82](catalog-04-io-modulos-y-sistema.md#nx82-función-usada-sin-importar) | Función usada sin importar | Módulos |
| [NX83](catalog-04-io-modulos-y-sistema.md#nx83-extensión-de-archivo-inválida-en-inject) | Extensión de archivo inválida en `#inject` | Módulos |
| [NX84](catalog-04-io-modulos-y-sistema.md#nx84-símbolo-no-encontrado-en-el-módulo-importado) | Símbolo no encontrado en el módulo importado | Módulos |
| [NX90](catalog-04-io-modulos-y-sistema.md#nx90-error-de-sintaxis) | Error de sintaxis | Sintaxis |
| [NX91](catalog-04-io-modulos-y-sistema.md#nx91-comentario-o-cadena-mal-cerrada) | Comentario o cadena mal cerrada | Sintaxis |
| [NX92](catalog-04-io-modulos-y-sistema.md#nx92-desbordamiento-de-pila-o-memoria) | Desbordamiento de pila o memoria | Sistema |
| [NX99](catalog-04-io-modulos-y-sistema.md#nx99-error-interno-del-lenguaje) | Error interno del lenguaje | Sistema |

---


## Categorías del catálogo

| Categoría | Códigos | Documento |
|-----------|---------|-----------|
| Variables, constantes y tipos | NX00–NX19 | [Variables, constantes y tipos (NX00–NX19)](catalog-01-variables-y-tipos.md) |
| Control de flujo y funciones | NX20–NX39 | [Control de flujo y funciones (NX20–NX39)](catalog-02-control-y-funciones.md) |
| Manejo de errores y colecciones | NX40–NX59 | [Manejo de errores y colecciones (NX40–NX59)](catalog-03-errores-y-colecciones.md) |
| Entrada/salida, módulos, red y sistema | NX60–NX99 | [Entrada/salida, módulos, red y sistema (NX60–NX99)](catalog-04-io-modulos-y-sistema.md) |

> El catálogo está dividido en cuatro documentos para mantener cada
> archivo por debajo de ~800 líneas y facilitar su mantenimiento.

---

## Tipos de excepción y su código NX

Los códigos `NX` describen la **causa raíz** de un error. Cuando capturas
errores con `try/catch`, los `catch` usan **tipos de excepción** que agrupan
varios códigos:

| Tipo de excepción | Código NX principal |
|-------------------|---------------------|
| `ErrorDivision` | NX01 |
| `ErrorIndice` | NX11 |
| `ErrorTipo` | NX07, NX10, NX12, NX33 |
| `ErrorMemoria` | NX92 |
| `ErrorArchivo` | NX61, NX62 |
| `ErrorEntrada` | NX60 |
| `ErrorValidacion` | NX12, NX60 |
| `ErrorRed` | NX70 |
| `ErrorGrafico` | NX71 |
| `ErrorAssert` | NX44 |
| `ErrorMatematico` | NX01, NX13 |

`Error` es la base de todos ellos: un `catch (Error e)` captura cualquier
error no capturado antes por un `catch` más específico.

---

## Buenas prácticas generales

1. **Lee el código en el mensaje de error:** identifica la línea exacta antes de buscar la solución.
2. **Agrupa errores por categoría:** los códigos `NX00–NX09` son de variables, `NX10–NX19` de tipos, `NX20–NX29` de control de flujo, `NX30–NX39` de funciones, `NX40–NX49` de manejo de errores, `NX50–NX59` de colecciones, `NX60–NX69` de E/S y archivos, `NX70–NX79` de red/gráficos, `NX80–NX89` de módulos y `NX90–NX99` de sintaxis y sistema.
3. **Documenta qué errores puede lanzar cada función tuya:** ayuda a quien consuma tu código y a ti mismo.
4. **Se específico en los mensajes:** al lanzar `ErrorValidacion("...")`, describe exactamente el problema.
