# Catálogo rápido de errores NX

Esta página es un **índice de consulta rápida**. El catálogo completo,
con descripción, causa, ejemplo, solución paso a paso y prevención de
cada código, está en
[`language/errors/errors.md`](language/errors/errors.md).

## Variables y constantes (NX00–NX09)

| Código | Error |
|--------|-------|
| NX00 | Variable no inicializada |
| NX01 | División por cero |
| NX02 | Variable no definida |
| NX03 | Reasignación de constante |
| NX04 | Declaración duplicada |
| NX05 | Identificador inválido |
| NX06 | Constante sin inicializar |
| NX07 | Tipo incompatible en asignación |
| NX08 | Variable `auto` sin inicializador |
| NX09 | Valor fuera del rango del tipo |

## Tipos y evaluación (NX10–NX19)

| Código | Error |
|--------|-------|
| NX10 | Operandos con tipos incompatibles |
| NX11 | Índice fuera de rango |
| NX12 | Conversión de tipo inválida |
| NX13 | Operación matemática inválida |
| NX14 | Tipo de retorno incompatible |
| NX15 | Tipo no reconocido |
| NX16 | Carácter inválido |
| NX17 | Índice o clave de tipo inválido |
| NX18 | Comparación entre tipos incompatibles |
| NX19 | Desbordamiento aritmético en ejecución |

## Control de flujo (NX20–NX29)

| Código | Error |
|--------|-------|
| NX20 | `break` fuera de un bucle |
| NX21 | `continue` fuera de un bucle |
| NX22 | Paso de bucle inválido |
| NX23 | Condición no booleana |
| NX24 | Caso duplicado en `switch` |
| NX25 | `case` o `default` fuera de `switch` |
| NX26 | `default` duplicado en `switch` |
| NX27 | Rango de `case` invertido |
| NX28 | Valor de `case` con tipo distinto al del `switch` |
| NX29 | Límites o paso del `for` no numéricos |

## Funciones (NX30–NX39)

| Código | Error |
|--------|-------|
| NX30 | Ruta sin retorno en función |
| NX31 | Falta tipo de retorno |
| NX32 | Cantidad de argumentos incorrecta |
| NX33 | Tipo de argumento incorrecto |
| NX34 | Función declarada dos veces |
| NX35 | Parámetro repetido en la firma |
| NX36 | `emit` en función `void` |
| NX37 | `emit` fuera de una función |

## Manejo de errores (NX40–NX49)

| Código | Error |
|--------|-------|
| NX40 | `catch` sin `try` previo |
| NX41 | `try` vacío |
| NX42 | Error no capturado |
| NX43 | Lanzar un valor que no es `Error` |
| NX44 | Aserción fallida |
| NX45 | `catch` con tipo que no es `Error` |
| NX46 | `catch` sin variable |

## Colecciones (NX50–NX59)

| Código | Error |
|--------|-------|
| NX50 | Operación sobre colección vacía |
| NX51 | Modificar colección durante iteración |
| NX52 | Clave no encontrada en `Map` |
| NX53 | Operación no soportada por la colección |

## Entrada/Salida y archivos (NX60–NX69)

| Código | Error |
|--------|-------|
| NX60 | Formato de entrada inválido |
| NX61 | Archivo no encontrado |
| NX62 | Error de lectura/escritura |
| NX63 | Directorio no encontrado al listar |

## Red y gráficos (NX70–NX79)

| Código | Error |
|--------|-------|
| NX70 | Error de red |
| NX71 | Error gráfico |

## Módulos e importación (NX80–NX89)

| Código | Error |
|--------|-------|
| NX80 | Módulo no encontrado |
| NX81 | Importación circular |
| NX82 | Función usada sin importar |
| NX83 | Extensión de archivo inválida en `#inject` |
| NX84 | Símbolo no encontrado en el módulo importado |

## Sintaxis y sistema (NX90–NX99)

| Código | Error |
|--------|-------|
| NX90 | Error de sintaxis |
| NX91 | Comentario o cadena mal cerrada |
| NX92 | Desbordamiento de pila o memoria |
| NX99 | Error interno del lenguaje |
