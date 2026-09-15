# 🚀 Instalación de Nexis

Guía oficial paso a paso para instalar **Nexis** (compilador `nexisc` + intérprete `nexisi`) en tu equipo. Elige tu sistema operativo y sigue los pasos en orden.

## Qué incluye el instalador

- El **compilador** `nexisc` y el **intérprete** `nexisi`.
- La **documentación** oficial del lenguaje.
- La **suite de tests** del lenguaje.
- La **extensión de VS Code** (`.vsix`).

> La versión actual es una **demo**: la implementación cubre tipos, operadores, `Console` e interpolación `fs"…"`. El alcance completo (control de flujo, funciones, POO, `try/catch` y módulos) llegará con **Nexis V1.0.0**.

---

## 📥 1. Descarga previa

Antes de nada, descarga el instalador **para tu sistema** a la carpeta de **Descargas**:

| Versión | Estado | Windows | Linux |
|---|---|---|---|
| **v0.0.2** (recomendada) | Publicada (demo) | [nexis-v0.0.2-windows-x86_64.exe](v0.0.2/nexis-v0.0.2-windows-x86_64.exe) | **Debian/Ubuntu:** [nexis-v0.0.2-linux-x86_64.deb](v0.0.2/nexis-v0.0.2-linux-x86_64.deb) <br> **Otras distros:** [nexis-v0.0.2-linux-x86_64.tar.xz](v0.0.2/nexis-v0.0.2-linux-x86_64.tar.xz) |
| v0.0.1 | Publicada (demo) | [nexis-v0.0.1-windows-x86_64.exe](v0.0.1/nexis-v0.0.1-windows-x86_64.exe) | **Debian/Ubuntu:** [nexis-v0.0.1-linux-x86_64.deb](v0.0.1/nexis-v0.0.1-linux-x86_64.deb) <br> **Otras distros:** [nexis-v0.0.1-linux-x86_64.tar.xz](v0.0.1/nexis-v0.0.1-linux-x86_64.tar.xz) |

> **macOS:** el instalador `.pkg` está pendiente (debe generarse en un equipo Mac).

---

## 🐧 2. Linux — Debian/Ubuntu (`.deb`)

Estos pasos son para **Debian**, **Ubuntu** o cualquier distro compatible con paquetes `.deb`.

### Paso 1 — Descarga el archivo

Con el navegador, descarga [nexis-v0.0.2-linux-x86_64.deb](v0.0.2/nexis-v0.0.2-linux-x86_64.deb). El archivo quedará en tu carpeta de **Descargas** (`~/Descargas`).

### Paso 2 — Abre una terminal

Pulsa `Ctrl + Alt + T` (o abre la app *Terminal* en el menú). Navega a la carpeta donde lo descargaste:

```bash
cd ~/Descargas
ls -lh nexis-v0.0.2-linux-x86_64.deb
```

Debes ver el archivo con su tamaño. Si lo guardaste en otra carpeta, usa `cd` a esa ruta.

### Paso 3 — Ejecuta el comando de instalación

```bash
sudo dpkg -i nexis-v0.0.2-linux-x86_64.deb
```

Se te pedirá la contraseña de tu usuario. Verás la salida:

```
(Reading database ... files and directories currently installed.)
Preparing to unpack nexis-v0.0.2-linux-x86_64.deb ...
Unpacking nexis (0.0.2) ...
Setting up nexis (0.0.2) ...
```

> **Dependencias:** si aparece un mensaje de dependencias sin cumplir, ejecuta después `sudo apt-get install -f -y` y vuelve a comprobar.

### Paso 4 — Comprueba el PATH

El paquete `.deb` instala los binarios en `/usr/local/bin/`, una carpeta **ya incluida en el PATH** de Debian/Ubuntu. Verifícalo:

```bash
echo $PATH
```

Si la salida contiene `/usr/local/bin`, no hace falta nada más. Si no lo contiene, añádelo (las comillas van exactas):

```bash
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### Paso 5 — Verifica la instalación

```bash
nexisc --version
nexisi --version
```

Cada comando debe imprimir la versión **igual a la del paquete instalado**, p. ej. `nexisc 0.0.2 (Nexis)`. Para saber exactamente desde dónde se ejecuta:

```bash
which nexisc
which nexisi
```

Deben apuntar a `/usr/local/bin/nexisc` y `/usr/local/bin/nexisi`. Si alguna vez aparece `command not found`, vuelve al paso 4 (o abre una terminal nueva).

> **Atención:** si instalaste antes la versión `.tar.xz` (via `install.sh`), puede quedar una copia antigua en `~/.local/bin` que **gana** a `/usr/local/bin` porque `~/.local/bin` está primero en el `PATH`. Compruébalo con `which nexisc` (si apunta a `~/.local/bin`, esa copia manda) y elimina las copias sobrantes:
> ```bash
> rm -f ~/.local/bin/nexisc ~/.local/bin/nexisi
> hash -r
> ```
> En el `PATH` también pueden quedar entradas duplicadas de `~/.local/bin` (las añade `install.sh` cada vez que se ejecuta); son inocuas pero conviene limpiarlas en `~/.bashrc`.

### Paso 6 — Prueba el lenguaje

Crea un archivo `hola.nxs`:

```nexis
Console.print("Hola, mundo")
```

Y ejecútalo:

```bash
nexisi hola.nxs
```

Salida esperada:

```
Hola, mundo
```

---

## 🐧 3. Linux — Otras distribuciones (`.tar.xz`)

Para distros que no usan `.deb` (Fedora, Arch, openSUSE, …) se usa el paquete comprimido con su instalador `install.sh`.

### Paso 1 — Descarga el archivo

Descarga [nexis-v0.0.2-linux-x86_64.tar.xz](v0.0.2/nexis-v0.0.2-linux-x86_64.tar.xz) a tu carpeta de **Descargas** (`~/Descargas`).

### Paso 2 — Abre una terminal y descomprime

```bash
cd ~/Descargas
tar -xJf nexis-v0.0.2-linux-x86_64.tar.xz
cd nexis-v0.0.2-linux-x86_64
```

Revisa el contenido:

```bash
ls -la
```

Verás `install.sh`, `uninstall.sh`, `bin/` (con `nexisc` y `nexisi`) y `docs/`.

### Paso 3 — Ejecuta el instalador

Instalación **para tu usuario** (recomendada):

```bash
./install.sh
```

Esto copia los binarios a `~/.local/bin/` y la documentación a `~/.local/share/doc/nexis`. El propio instalador **añade `~/.local/bin` al PATH** en tu `~/.bashrc` (o `~/.zshrc`) y te lo indica al final.

> **Instalación global** (para todos los usuarios del sistema): `sudo ./install.sh /usr/local`. En ese caso los binarios van a `/usr/local/bin/`, que ya está en el PATH.

### Paso 4 — Actualiza el PATH y recarga la shell

El instalador ya escribió la línea en tu archivo, pero **hasta que recargues la shell no tendrá efecto**. Ejecuta:

```bash
source ~/.bashrc
```

(O `source ~/.zshrc` si usas Zsh. También vale abrir una **nueva ventana de terminal**.)

Si prefieres añadirlo a mano, la línea que se debe agregar es:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### Paso 5 — Verifica la instalación

```bash
nexisc --version
nexisi --version
which nexisc    # debe mostrar ~/.local/bin/nexisc o /usr/local/bin/nexisc
```

> Si ejecutaste `sudo ./install.sh /usr/local`, comprueba con `echo $PATH` que `/usr/local/bin` esté listado (lo está por defecto en casi todas las distros).

### Paso 6 — Prueba el lenguaje

```nexis
Console.print("Hola, mundo")
```

```bash
nexisi hola.nxs
```

Salida esperada:

```
Hola, mundo
```

---

## 🪟 4. Windows (`.exe`)

### Paso 1 — Descarga el archivo

Descarga [nexis-v0.0.2-windows-x86_64.exe](v0.0.2/nexis-v0.0.2-windows-x86_64.exe) a tu carpeta de **Descargas**.

### Paso 2 — Ejecuta el instalador

Haz doble clic sobre el `.exe` (o clic derecho → *Ejecutar como administrador*) y sigue el **asistente de instalación (NSIS)**. El instalador:

- Instala Nexis en `%LOCALAPPDATA%\Nexis` (binarios en `%LOCALAPPDATA%\Nexis\bin`).
- **Añade `bin\` al PATH** de tu usuario automáticamente.
- Deja la documentación y la extensión de VS Code en la carpeta de instalación.

### Paso 3 — Abre una ventana nueva de PowerShell

El PATH solo se actualiza en las **nuevas** ventanas que se abran después de instalar. Abre una ventana nueva (Inicio → *PowerShell*) y verifica:

```powershell
nexisc --version
nexisi --version
```

También puedes comprobar desde dónde se ejecuta:

```powershell
Get-Command nexisc | Select-Object Source
```

Debe mostrar una ruta con `...\Nexis\bin\nexisc.exe`.

> **Si da `command not found`:** abre una ventana totalmente nueva, o reinicia el equipo si acabas de instalar por primera vez. También puedes usar el binario directamente: `cd $env:LOCALAPPDATA\Nexis\bin` y luego `.\nexisc.exe --version`.

### Paso 4 — Prueba el lenguaje

Crea `hola.nxs`:

```nexis
Console.print("Hola, mundo")
```

```powershell
nexisi hola.nxs
```

Salida esperada:

```
Hola, mundo
```

---

## 🔄 5. Actualizar a una nueva versión

Cuando salga una versión más nueva, **no hace falta desinstalar la anterior**: basta con instalar la versión nueva sobre la actual.

### Linux (`.deb`)

```bash
cd ~/Descargas
sudo dpkg -i nexis-nueva-version-linux-x86_64.deb
```

`dpkg` reemplaza los archivos anteriores automáticamente.

### Linux (`.tar.xz`)

```bash
cd ~/Descargas
tar -xJf nexis-nueva-version-linux-x86_64.tar.xz
cd nexis-nueva-version-linux-x86_64
./install.sh        # sobrescribe los binarios en ~/.local/bin
source ~/.bashrc
```

### Windows

Descarga el nuevo `.exe` y ejecútalo: el asistente instala sobre la versión anterior.

### Tras cualquier actualización: verifica

```bash
nexisc --version && which nexisc
nexisi --version && which nexisi
```

- Ambos comandos deben responder con la **versión del paquete** que acabas de instalar (`v0.0.2` imprime `0.0.2`, etc.).
- `which` debe apuntar a la carpeta de instalación (no a una copia antigua que ya tuvieras en el PATH, p. ej. `~/.local/bin`).
- Si la shell «recuerda» la ubicación antigua, ejecuta `hash -r` (Bash) o abre una ventana nueva.
- Si instalas de nuevo una versión **ya instalada** (p. ej. por un paquete corregido), `sudo dpkg -i` la reemplaza igualmente: verás `Desempaquetando nexis (0.0.2) sobre (0.0.2) ...` y no hace falta desinstalar antes.

---

## 🗑️ 6. Desinstalar

### Linux (`.deb`)

```bash
sudo dpkg -r nexis
```

(o `sudo apt remove nexis`). Esto elimina los binarios y la documentación.

### Linux (`.tar.xz`)

Desde la carpeta extraída:

```bash
./uninstall.sh                      # instalación de usuario
sudo ./uninstall.sh /usr/local      # instalación global
```

El desinstalador borra los binarios, la documentación y la línea del PATH que añadió `install.sh`. Para limpiar del todo, cierra y reabre la terminal.

### Windows

- **Panel de configuración** → *Aplicaciones* → *Aplicaciones instaladas* → busca **Nexis** → *Desinstalar*.
- O reinicia el instalador `.exe`, que ofrece la opción de eliminar.
- Si el PATH quedó con la carpeta `Nexis\bin`, quítala en *Editar las variables de entorno del sistema* → *Variables de entorno*.

---

## ❓ 7. Solución de problemas

| Problema | Causa probable | Solución |
|---|---|---|
| `nexisc: command not found` | El PATH no se ha recargado o la carpeta no está en el PATH | Reabre la terminal o `source ~/.bashrc`; comprueba con `echo $PATH` |
| Sigue la versión antigua | La shell recuerda la ubicación previa, o hay dos copias en el PATH (una en `~/.local/bin` y otra en `/usr/local/bin`) | `hash -r` (Bash); `which nexisc` para ver cuál gana; `rm -f ~/.local/bin/nexisc ~/.local/bin/nexisi` y reinstala |
| `nexisc --version` no coincide con el paquete instalado | Binarios con la versión grabada desactualizada | Descarga el instalador **corregido** de [installer/](README.md) y vuelve a instalarlo (ver «Actualizar a una nueva versión») |
| `sudo dpkg -i` falla por dependencias | Paquetes requeridos sin instalar | `sudo apt-get install -f -y` |
| En PowerShell sale `not found` | La ventana se abrió antes de instalar | Abre una ventana nueva o `cd $env:LOCALAPPDATA\Nexis\bin` |
| El binario no se ejecuta por permisos (Linux/`.tar.xz`) | Falta el bit de ejecución | `chmod +x ~/.local/bin/nexisc ~/.local/bin/nexisi` |

---

## 🧩 8. Extensión de VS Code

### Última versión (v0.0.2 — recomendada)

Gramática realineada con la documentación, `fs"…"`, `#inject`, 20 snippets e icono propio:

1. Descarga [nexis-0.0.2.vsix](../releases/extension/v0.0.2/nexis-0.0.2.vsix).
2. En VS Code abre la paleta de comandos (`Ctrl+Shift+P`).
3. Ejecuta *Extensions: Install from VSIX...* y selecciona el archivo.

### Incluida en el instalador

El paquete del producto `v0.0.2` lleva la extensión actualizada (`nexis-0.0.2.vsix`).

---

## 📦 Publicar una nueva versión

1. Genera los instaladores por plataforma (Linux y Windows; macOS cuando haya un Mac disponible).
2. Añade los artefactos a `installer/<versión>/` y a [releases/nexis/](../releases/nexis/README.md) como `nexis-<versión>-<plataforma>.<ext>`.
3. Actualiza la tabla de estado de este documento y el [índice de releases](../releases/README.md).