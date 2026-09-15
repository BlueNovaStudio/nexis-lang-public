# 📥 Instalación de Nexis (`nexisc`)

Guía oficial para instalar el compilador **`nexisc`** desde el `.zip` descargado. Compatible con **Linux**, **Windows** (PowerShell) y **macOS**.

## Qué recibes

Al descomprimir `nexisc-v<VERSIÓN>-<plataforma>.zip` obtienes el ejecutable `nexisc` (en Windows, `nexisc.exe`). Es un binario único, no necesita instalar runtime ni dependencias.

> Reemplaza `<VERSIÓN>` por la versión que descargaste (ej: `nexisc-v0.0.1-x86_64.zip`) y `<URL-DEL-ZIP>` por la dirección de descarga.

---

## 🐧 Linux

### 1. Descargar y descomprimir

```bash
wget <URL-DEL-ZIP>/nexisc-v<VERSIÓN>-x86_64.zip
unzip nexisc-v<VERSIÓN>-x86_64.zip -d nexisc
cd nexisc
```

Si no tienes `unzip`: `sudo apt install unzip`

### 2. Instalar en tu carpeta personal

```bash
mkdir -p ~/.local/bin
install -m 755 nexisc ~/.local/bin/
```

### 3. Añadir al PATH (una sola vez)

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### 4. Verificar

```bash
nexisc --version
```

Si prefieres una instalación global (para todos los usuarios del sistema): `sudo install -m 755 nexisc /usr/local/bin/`

---

## 🪟 Windows (PowerShell)

### 1. Descargar y descomprimir

```powershell
Invoke-WebRequest -Uri "<URL-DEL-ZIP>/nexisc-v<VERSIÓN>-windows-x86_64.zip" -OutFile "$env:USERPROFILE\nexisc.zip"
Expand-Archive "$env:USERPROFILE\nexisc.zip" -DestinationPath "$env:USERPROFILE\nexisc"
```

### 2. Añadir al PATH (una sola vez)

```powershell
[Environment]::SetEnvironmentVariable("Path", "$env:USERPROFILE\nexisc;" + [Environment]::GetEnvironmentVariable("Path", "Machine"), "User")
```

### 3. Nueva sesión y verificar

Abre una **nueva** ventana de PowerShell y ejecuta:

```powershell
nexisc --version
```

> También puedes usar `nexisc.exe` directamente sin tocar el PATH: `cd $env:USERPROFILE\nexisc` y después `.\nexisc.exe --version`.

Para **desinstalar**: borra la carpeta `%USERPROFILE%\nexisc` y elimina esa entrada del PATH en Configuración > Sistema > Opciones avanzadas > Variables de entorno.

---

## 🍎 macOS

### 1. Descargar y descomprimir

```bash
curl -O <URL-DEL-ZIP>/nexisc-v<VERSIÓN>-mac-x86_64.zip
unzip nexisc-v<VERSIÓN>-mac-x86_64.zip -d nexisc
cd nexisc
```

### 2. Instalar globalmente

```bash
sudo mkdir -p /usr/local/bin
sudo install -m 755 nexisc /usr/local/bin/
```

### 3. Verificar

```bash
nexisc --version
```

> **Gatekeeper:** si macOS bloquea el binario por venir de internet, quita la marca de cuarentena:
> `xattr -d com.apple.quarantine /usr/local/bin/nexisc`

---

## ✅ Probarlo

Crea un archivo `hola.nxs`:

```python
Console.print("Hola, mundo")
```

Y ejecútalo:

```bash
nexisc hola.nxs
```

Salida esperada:

```
Hola, mundo
```

## ❓ Ayuda

```bash
nexisc --help
```

- Códigos de error `NX` explicados en [el catálogo de errores](language/errors/errors.md).
- Documentación completa del lenguaje en [`docs/`](README.md).