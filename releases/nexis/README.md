# Nexis — Producto completo

Esta carpeta guarda las **versiones del lenguaje Nexis como producto completo** (el «todo»): la versión de Nexis que un usuario normal buscaría instalar, que agrupa:

- Documentación y tests (`docs/` y artefactos de tests en `releases/docs/`)
- Extensión de VS Code (`releases/extension/`)
- Compilador (`compiler/`)
- Intérprete (`interpreter/`)

Cada release se sube como un único artefacto comprimido, por ejemplo `nexis-v1.0.0.zip`.

## Estado

| Versión | Estado |
|---|---|
| **V1.0.0** | No publicada. Pendiente de que existan `compiler/` e `interpreter/`. |

Cuando se publique la primera versión completa:

1. Crea `releases/nexis/<versión>/` y comprime todo el proyecto (o los artefactos finales) como `nexis-<versión>.zip`.
2. Añade un `README.md` describiendo qué incluye esa versión y qué soluciona respecto a la anterior.
3. Actualiza el [índice de releases](../README.md).