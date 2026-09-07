# 💬 Comentarios en Nexis

Los comentarios permiten añadir notas explicativas al código sin que afecten su ejecución. Nexis soporta comentarios de una línea y de varias líneas.

## 1. Comentario de una línea

Usa `#/` seguido del texto. Todo lo que esté después de `#/` hasta el final de la línea se ignora.

```
#/ Esto es un comentario de una línea
int edad = 18  #/ y un comentario al final de la línea
```

También se admite `//` como atajo:

```
// Este comentario también es válido
```

## 2. Comentario de varias líneas

### Con `#/* ... */#`

```
#/*
Esto es un comentario
que ocupa varias líneas
y se ignora por completo
*/#
```

### Con `/* ... */`

```
/*
También puedes usar el delimitador clásico
para varias líneas
*/
```

### Con `#{ ... }#`

```
#{
Una tercera forma de comentario de bloque
}#
```

## 3. Reglas

1. Los comentarios de bloque no pueden anidarse: un `#/*` dentro de otro `#/* ... */#` no es válido y generará un error de sintaxis (NX90) o un comentario mal cerrado (NX91).
2. Cierra siempre los comentarios de bloque; olvidar el delimitador de cierre produce [NX91](../errors/errors.md#nx91-comentario-o-cadena-mal-cerrada).

## 4. Buenas prácticas

- Explica el **porqué** de una decisión, no "qué" hace el código (que ya es obvio leyéndolo).
- Mantén los comentarios al día; un comentario desactualizado confunde más que un código sin comentarios.
- Usa comentarios para marcar secciones o ejercicios (por ejemplo, en los archivos de prueba se usa `#/ NX02: variable no definida`).