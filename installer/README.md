# 🚀 Instalador de Nexis

Este directorio albergará los **instaladores oficiales** del lenguaje Nexis para llevar el compilador y el intérprete a tu equipo con un solo clic.

## Estado actual

| Componente | Estado |
|---|---|
| Instalador del lenguaje | 🚧 En desarrollo |
| **Nexis V1.0.0** | ⏳ Pendiente del compilador y el intérprete |

El instalador completo incluirá:

- El **intérprete** (`nexis` en línea de comandos).
- El **compilador** (cuando esté publicado).
- Integración con Visual Studio Code a través de la extensión oficial.

## Mientras tanto, qué puedes instalar hoy

### Extensión de VS Code (disponible)

Da resaltado de sintaxis, comentarios y consola para Nexis:

1. Descarga el paquete desde [releases/extension/v0.0.1](../../releases/extension/v0.0.1/nexis-programming-language-support-0.0.1.vsix).
2. En VS Code abre la paleta de comandos (`Ctrl+Shift+P`).
3. Ejecuta *Extensions: Install from VSIX...* y selecciona el archivo.

### Documentación (disponible)

Toda la documentación oficial está disponible en [docs/](../docs/README.md) y los ejemplos en [examples/](../examples/README.md).

## Proceso para publicar el primer instalador

Cuando exista el compilador **y** el intérprete:

1. Empaqueta el ejecutable y sus dependencias en un instalador por plataforma (Windows, Linux y macOS).
2. Añade el artefacto a [releases/nexis/](../releases/nexis/README.md) como `nexis-<versión>.zip`.
3. Libera la primera versión completa **Nexis V1.0.0** y publica el enlace aquí.