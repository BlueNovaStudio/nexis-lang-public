# 📦 Módulos e importación en Nexis

Los módulos permiten reutilizar código separándolo en archivos. Nexis usa la directiva `#inject` para importar librerías nativas o archivos propios.

## Contenido

- [Implementación de librerías o ficheros](imports.md) — `#inject`, librerías nativas y archivos locales.

## En esta sección aprenderás

- Importar librerías nativas (`math`, `vector`, `string`, etc.).
- Importar tus propios archivos `.nex`.
- Organizar un proyecto en varios módulos.

## Referencia rápida

```nexis
#inject math;
#inject "utilidades/calculos.nex";

float area = math.PI * math.pow(radio, 2)
```

## Reglas importantes

1. Las directivas `#inject` van al **inicio** del archivo.
2. Cada directiva termina con `;`.
3. Las librerías nativas se escriben sin comillas; los archivos propios, con `"ruta.nex"`.
4. Evita importaciones circulares (NX81) e importa solo lo que usas.

## Errores relacionados

- [NX80](../errors/errors.md#nx80-módulo-no-encontrado): el módulo no existe.
- [NX81](../errors/errors.md#nx81-importación-circular): dependencia circular.
- [NX82](../errors/errors.md#nx82-función-usada-sin-importar): usar una función sin importarla.