# 🧩 Manejo de errores en Nexis

En Nexis, los errores se identifican con un **código único de formato `NXXX`** (ej. `NX01`, `NX42`) que aparece junto al mensaje de error cuando el programa se detiene. Este código te lleva directo a la solución.

## Cómo se agrupan los códigos

| Rango | Categoría |
|-------|-----------|
| `NX00–NX09` | Variables y constantes |
| `NX10–NX19` | Tipos y evaluación |
| `NX20–NX29` | Control de flujo |
| `NX30–NX39` | Funciones |
| `NX40–NX49` | Manejo de errores |
| `NX50–NX59` | Colecciones |
| `NX60–NX69` | Entrada/salida y archivos |
| `NX70–NX79` | Red y gráficos |
| `NX80–NX89` | Módulos e importación |
| `NX90–NX99` | Sintaxis y sistema |

## Códigos documentados

| Código | Error |
|--------|-------|
| `NX00` | Variable no inicializada |
| `NX01` | División por cero |
| `NX02` | Variable no definida |
| `NX03` | Reasignación de constante |
| `NX04` | Declaración duplicada |
| `NX05` | Identificador inválido |
| `NX06` | Constante sin inicializar |
| `NX07` | Tipo incompatible en asignación |
| `NX10` | Operandos con tipos incompatibles |
| `NX11` | Índice fuera de rango |
| `NX12` | Conversión de tipo inválida |
| `NX13` | Operación matemática inválida |
| `NX20` | `break` fuera de un bucle |
| `NX21` | `continue` fuera de un bucle |
| `NX22` | Paso de bucle inválido |
| `NX23` | Condición no booleana |
| `NX24` | Caso duplicado en `switch` |
| `NX30` | Ruta sin retorno en función |
| `NX31` | Falta tipo de retorno |
| `NX32` | Cantidad de argumentos incorrecta |
| `NX33` | Tipo de argumento incorrecto |
| `NX34` | Función declarada dos veces |
| `NX35` | Parámetro repetido en la firma |
| `NX40` | `catch` sin `try` previo |
| `NX41` | `try` vacío |
| `NX42` | Error no capturado |
| `NX43` | Lanzar un valor que no es `Error` |
| `NX44` | Aserción fallida |
| `NX50` | Operación sobre colección vacía |
| `NX51` | Modificar colección durante iteración |
| `NX60` | Formato de entrada inválido |
| `NX61` | Archivo no encontrado |
| `NX62` | Error de lectura/escritura |
| `NX70` | Error de red |
| `NX71` | Error gráfico |
| `NX80` | Módulo no encontrado |
| `NX81` | Importación circular |
| `NX82` | Función usada sin importar |
| `NX90` | Error de sintaxis |
| `NX91` | Comentario o cadena mal cerrada |
| `NX92` | Desbordamiento de pila o memoria |
| `NX99` | Error interno del lenguaje |

## Relación con los tipos de excepción

Los códigos `NX` describen la **causa-raíz** de un error. Cuando capturas errores en `try/catch`, los `catch` usan **tipos de excepción** que se corresponden con varios códigos:

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

## Contenido relacionado

- [Catálogo completo de errores NX](errors.md) — descripción, causa, ejemplo, solución paso a paso y prevención de cada código.
- [Try/Catch](try_catch.md) — cómo capturar, lanzar y depurar errores.

## Antes de buscar un código

1. **Localiza la línea** que indica el mensaje de error.
2. **Lee el nombre de la variable o función** involucrada.
3. Busca el código en este índice y usa la categoría como pista inicial.