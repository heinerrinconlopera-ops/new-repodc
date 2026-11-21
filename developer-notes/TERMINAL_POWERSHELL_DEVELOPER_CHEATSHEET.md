# Terminal & PowerShell Cheat Sheet para Developers

> **Guía de referencia para trabajar profesionalmente desde Windows Terminal / PowerShell y VS Code.**
>
> En esta guía, los ejemplos están escritos principalmente para **PowerShell en Windows 10/11**. No todos los comandos funcionan igual en CMD, Bash, macOS o Linux. Cuando una diferencia sea importante, se indica.

---

## Índice

1. [Qué es la terminal y cómo pensar como developer](#1-qué-es-la-terminal-y-cómo-pensar-como-developer)
2. [Cómo leer y escribir comandos](#2-cómo-leer-y-escribir-comandos)
3. [Los comandos que más vas a usar](#3-los-comandos-que-más-vas-a-usar)
4. [Moverte por carpetas y rutas](#4-moverte-por-carpetas-y-rutas)
5. [Crear, copiar, mover y borrar archivos](#5-crear-copiar-mover-y-borrar-archivos)
6. [Leer, buscar y analizar archivos](#6-leer-buscar-y-analizar-archivos)
7. [Pipes, redirecciones y encadenar comandos](#7-pipes-redirecciones-y-encadenar-comandos)
8. [Procesos, programas y puertos](#8-procesos-programas-y-puertos)
9. [Variables de entorno y PATH](#9-variables-de-entorno-y-path)
10. [Node.js, npm y proyectos JavaScript](#10-nodejs-npm-y-proyectos-javascript)
11. [Python y entornos virtuales](#11-python-y-entornos-virtuales)
12. [Git y GitHub desde la terminal](#12-git-y-github-desde-la-terminal)
13. [SSH, autenticación y conexiones remotas](#13-ssh-autenticación-y-conexiones-remotas)
14. [Instalar herramientas y paquetes](#14-instalar-herramientas-y-paquetes)
15. [Diagnóstico de errores](#15-diagnóstico-de-errores)
16. [Seguridad: comandos peligrosos y hábitos profesionales](#16-seguridad-comandos-peligrosos-y-hábitos-profesionales)
17. [VS Code: terminal y productividad](#17-vs-code-terminal-y-productividad)
18. [Atajos de teclado](#18-atajos-de-teclado)
19. [Flujos de trabajo reales](#19-flujos-de-trabajo-reales)
20. [Comandos de Linux/macOS: equivalencias rápidas](#20-comandos-de-linuxmacos-equivalencias-rápidas)
21. [Glosario](#21-glosario)
22. [Plan para practicar](#22-plan-para-practicar)
23. [Checklist de consulta rápida](#23-checklist-de-consulta-rápida)

---

# 1. Qué es la terminal y cómo pensar como developer

La **terminal** es una interfaz de texto desde la que le das instrucciones al sistema operativo. En lugar de abrir carpetas y presionar botones, escribes comandos para navegar, crear archivos, ejecutar programas, instalar dependencias, revisar procesos y automatizar tareas.

### Terminal, shell y PowerShell no son exactamente lo mismo

- **Terminal:** la aplicación o ventana donde escribes y ves los comandos. Ejemplos: Windows Terminal y la terminal integrada de VS Code.
- **Shell:** el programa que interpreta tus comandos.
- **PowerShell:** una shell y lenguaje de automatización de Microsoft. Es la shell que usamos en los ejemplos de esta guía.
- **CMD:** la consola clásica de Windows. Su sintaxis es diferente en algunos comandos.
- **Bash/Zsh:** shells comunes en Linux y macOS.

### Qué puedes hacer desde la terminal

- Navegar por el sistema de archivos.
- Crear, editar, copiar, mover y eliminar archivos.
- Ejecutar tu código y servidores locales.
- Instalar paquetes y herramientas.
- Inspeccionar procesos y puertos.
- Configurar variables de entorno.
- Usar Git y herramientas de desarrollo.
- Automatizar tareas repetitivas mediante scripts.

### La regla de oro

**Antes de ejecutar un comando, verifica en qué carpeta estás y qué hará el comando.**

```powershell
Get-Location                 # Muestra la carpeta actual (pwd también funciona)
Get-ChildItem                # Lista los archivos de la carpeta (ls y dir también funcionan)
```

No ejecutes comandos destructivos si no entiendes el objetivo, la ruta o el alcance.

---

# 2. Cómo leer y escribir comandos

Un comando suele tener esta estructura:

```powershell
comando -opcion --otra-opcion argumento
```

Ejemplo:

```powershell
Get-ChildItem -Path . -File
```

- `Get-ChildItem`: comando que lista elementos.
- `-Path`: parámetro que indica la ruta.
- `.`: carpeta actual.
- `-File`: limita el resultado a archivos.

### Mayúsculas y minúsculas

PowerShell normalmente no distingue mayúsculas de minúsculas en nombres de comandos y parámetros. Aun así, escribe los nombres de forma consistente para facilitar su lectura.

### Rutas con espacios

Si una ruta contiene espacios, ponla entre comillas:

```powershell
Set-Location "C:\Users\Patron\Downloads\my first website"
```

Sin comillas, PowerShell puede interpretar cada palabra como un argumento separado.

### Rutas absolutas y relativas

- **Absoluta:** indica la ubicación completa, por ejemplo `C:\Users\Patron\Projects\website`.
- **Relativa:** se interpreta desde la carpeta actual, por ejemplo `..\api` o `src\components`.

Símbolos importantes:

| Símbolo | Significado |
|---|---|
| `.` | Carpeta actual |
| `..` | Carpeta superior |
| `~` | Carpeta del usuario (home) |
| `\` | Separador de carpetas en rutas de Windows |
| `*` | Comodín: coincide con varios nombres |
| `?` | Comodín: coincide con un carácter |
| `|` | Pipe: pasa el resultado de un comando al siguiente |

### Ayuda integrada

No necesitas memorizar cada parámetro. Consulta la ayuda:

```powershell
Get-Help Get-ChildItem
Get-Help Get-ChildItem -Examples
Get-Help Get-ChildItem -Full
Get-Command git
Get-Command python -All
```

Para muchos programas externos también funciona:

```powershell
git --help
node --help
npm --help
python --help
```

**Consejo:** usa `Tab` para completar nombres de archivos, carpetas y comandos. Reduce errores de escritura.

---

# 3. Los comandos que más vas a usar

Esta es la lista esencial para el trabajo diario:

| Comando | Para qué sirve | Frecuencia típica |
|---|---|---|
| `pwd` | Ver la carpeta actual | Constantemente |
| `ls` | Listar archivos y carpetas | Constantemente |
| `cd ruta` | Entrar en una carpeta | Constantemente |
| `cd ..` | Subir un nivel | Muy frecuente |
| `clear` | Limpiar la pantalla | Frecuente |
| `mkdir nombre` | Crear una carpeta | Frecuente |
| `New-Item archivo` | Crear un archivo | Frecuente |
| `code .` | Abrir la carpeta actual en VS Code | Frecuente |
| `git status` | Revisar cambios de Git | Constantemente en proyectos Git |
| `npm install` | Instalar dependencias de Node | Según el proyecto |
| `npm run dev` | Iniciar un servidor de desarrollo si existe ese script | Según el proyecto |
| `Ctrl + C` | Detener un programa que corre en la terminal | Frecuente |

> **Nota:** `pwd`, `ls`, `cd`, `clear` y `mkdir` son alias disponibles en PowerShell. Sus nombres completos son `Get-Location`, `Get-ChildItem`, `Set-Location`, `Clear-Host` y `New-Item` (para crear carpetas se usa `New-Item -ItemType Directory`).

---

# 4. Moverte por carpetas y rutas

## Ver dónde estás

```powershell
pwd
Get-Location
```

## Listar contenido

```powershell
ls                         # Lista la carpeta actual
ls -Force                  # Incluye elementos ocultos
ls -File                   # Solo archivos
ls -Directory              # Solo carpetas
ls -Name                   # Solo nombres
Get-ChildItem -Recurse     # Lista contenido de subcarpetas (puede ser largo)
```

## Cambiar de carpeta

```powershell
cd "C:\Users\Patron\Downloads"
cd ..                      # Subir una carpeta
cd .\src                   # Entrar en src desde la carpeta actual
cd ~                       # Ir a la carpeta del usuario
cd -                       # En algunas versiones/shells puede no comportarse como en Bash; usa una ruta explícita si falla
```

## Volver a una ruta usada recientemente

PowerShell mantiene un historial de ubicaciones:

```powershell
Get-Location
Push-Location "C:\Projects\website"  # Cambia de carpeta y guarda la anterior
Pop-Location                            # Vuelve a la ubicación guardada
```

## Buscar una carpeta por nombre

Desde una ubicación adecuada (por ejemplo, tu carpeta de usuario):

```powershell
Get-ChildItem -Path $HOME -Directory -Recurse -Filter "my first website" -ErrorAction SilentlyContinue
```

La búsqueda recursiva en toda la carpeta de usuario puede tardar. Limita el `-Path` a una carpeta concreta siempre que sea posible.

---

# 5. Crear, copiar, mover y borrar archivos

## Crear carpetas

```powershell
mkdir projects
New-Item -ItemType Directory -Path .\src
mkdir .\src\components
```

## Crear archivos vacíos

```powershell
New-Item -ItemType File -Path .\README.md
New-Item -ItemType File -Path .\src\index.js
```

Si el archivo ya existe, `New-Item` puede dar un error. Comprueba antes con `Test-Path`:

```powershell
Test-Path .\README.md
```

## Copiar archivos

```powershell
Copy-Item .\index.html .\index-backup.html
Copy-Item "$HOME\Downloads\GIT_GITHUB_CHEATSHEET.md" .
Copy-Item .\images .\public\images -Recurse
```

- `Copy-Item`: copia archivos o carpetas.
- `-Recurse`: incluye el contenido de subcarpetas.
- `.`: carpeta actual.

## Mover archivos

```powershell
Move-Item .\notes.txt .\docs\notes.txt
Move-Item .\draft.md .\README.md
```

## Cambiar nombre

```powershell
Rename-Item .\old-name.txt new-name.txt
```

## Borrar archivos o carpetas

```powershell
Remove-Item .\temporary.txt
Remove-Item .\old-folder -Recurse
```

**Mucho cuidado:** `Remove-Item` elimina elementos. Para revisar antes qué se borraría, utiliza `-WhatIf`:

```powershell
Remove-Item .\old-folder -Recurse -WhatIf
```

Si el resultado es exactamente lo que esperas, puedes repetir el comando sin `-WhatIf`.

Evita copiar comandos de eliminación con rutas que no hayas comprobado. Nunca ejecutes una eliminación recursiva desde `C:\`, `C:\Users` o la raíz de un proyecto sin saber exactamente qué selecciona.

---

# 6. Leer, buscar y analizar archivos

## Mostrar el contenido de un archivo

```powershell
Get-Content .\README.md
cat .\README.md              # Alias de Get-Content
Get-Content .\log.txt -Tail 30  # Últimas 30 líneas
Get-Content .\log.txt -Wait     # Sigue mostrando nuevas líneas (Ctrl+C para salir)
```

## Buscar texto dentro de archivos

```powershell
Select-String -Path .\*.html -Pattern "<title>"
Select-String -Path .\src\*.js -Pattern "TODO"
Get-ChildItem .\src -Recurse -File | Select-String -Pattern "console.log"
```

`Select-String` busca texto, similar a `grep` en Linux/macOS.

## Buscar archivos por nombre o extensión

```powershell
Get-ChildItem -Path . -Recurse -File -Filter "*.py"
Get-ChildItem -Path . -Recurse -File -Filter "*.md"
Get-ChildItem -Path . -Recurse -File -Include *.js,*.ts
```

## Contar líneas, palabras o elementos

```powershell
(Get-Content .\README.md).Count
Get-ChildItem .\src -Recurse -File | Measure-Object
```

## Ver el tipo de un archivo

```powershell
Get-Item .\index.html | Format-List Name,Length,LastWriteTime,FullName
```

---

# 7. Pipes, redirecciones y encadenar comandos

Estas herramientas te permiten construir flujos de trabajo con varios comandos.

## Pipe `|`

El pipe pasa los resultados de un comando al siguiente:

```powershell
Get-ChildItem | Sort-Object Length -Descending
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-ChildItem .\src -Recurse -File | Select-String "TODO"
```

Lee el ejemplo de izquierda a derecha: obtener procesos → ordenarlos por CPU → mostrar los primeros diez.

## Redirigir la salida a un archivo

```powershell
Get-ChildItem | Out-File .\files-list.txt
Get-Content .\log.txt | Out-File .\log-copy.txt
```

En PowerShell también puedes usar:

```powershell
"Build started" | Out-File .\build.log
"Another line" | Add-Content .\build.log
```

- `Out-File`: escribe la salida en un archivo y normalmente lo sobrescribe.
- `Add-Content`: agrega contenido al final.

Los operadores `>` y `>>` también redirigen salida, pero para controlar encoding y formato suele ser más claro usar `Out-File` / `Add-Content`.

## Ejecutar el siguiente comando solo si el anterior tuvo éxito

En PowerShell 7 o posterior:

```powershell
command1 && command2
```

En Windows PowerShell 5.1, usa una condición explícita:

```powershell
command1
if ($?) { command2 }
```

Para programas externos, consulta también `$LASTEXITCODE`:

```powershell
npm run build
$LASTEXITCODE
```

- `$?`: indica si la última operación de PowerShell tuvo éxito.
- `$LASTEXITCODE`: código de salida del último programa externo. Normalmente `0` significa éxito; otro número suele indicar error.

---

# 8. Procesos, programas y puertos

Cuando ejecutas un servidor de desarrollo, queda un proceso activo. Es útil saber identificarlo y detenerlo.

## Ver procesos

```powershell
Get-Process
Get-Process code
Get-Process node
Get-Process python
```

## Detener un programa desde la terminal

En la terminal donde está corriendo el servidor, presiona:

```text
Ctrl + C
```

Es la forma normal de detener `npm run dev`, un script de Python u otros procesos interactivos.

Si el proceso quedó en otra terminal:

```powershell
Get-Process node
Stop-Process -Name node
```

**Precaución:** `Stop-Process -Name node` detiene todos los procesos llamados `node` de tu usuario, lo que puede cerrar otros proyectos. Inspecciona antes y, si hace falta, termina un PID específico:

```powershell
Get-Process node | Select-Object Id,ProcessName,Path
Stop-Process -Id 12345
```

Reemplaza `12345` con el ID correcto. No detengas procesos del sistema que no reconozcas.

## Comprobar quién usa un puerto

Ejemplo: el servidor indica que el puerto `3000` ya está ocupado.

```powershell
Get-NetTCPConnection -LocalPort 3000 -ErrorAction SilentlyContinue
```

Para ver el proceso asociado:

```powershell
$connection = Get-NetTCPConnection -LocalPort 3000 -State Listen -ErrorAction SilentlyContinue
$connection | Select-Object LocalAddress,LocalPort,OwningProcess
Get-Process -Id $connection.OwningProcess
```

Si confirmas que es un proceso tuyo que puedes detener:

```powershell
Stop-Process -Id <PID>
```

Sustituye `<PID>` por el número real, sin escribir los símbolos `< >`.

## Ver información de red

```powershell
ipconfig
ipconfig /all
Test-NetConnection github.com -Port 443
```

`Test-NetConnection` ayuda a comprobar conectividad hacia un host y puerto.

---

# 9. Variables de entorno y PATH

Una **variable de entorno** es un valor que los programas pueden leer para conocer configuraciones del sistema, rutas, claves o el entorno en el que se ejecutan.

## Consultar variables

```powershell
$env:USERPROFILE
$env:HOME
$env:TEMP
$env:PATH
```

- `USERPROFILE`: carpeta de tu usuario de Windows.
- `TEMP`: carpeta temporal.
- `PATH`: lista de ubicaciones donde Windows busca ejecutables.

## Crear una variable temporal

```powershell
$env:MY_APP_MODE = "development"
$env:MY_APP_MODE
```

Esta variable existe en la sesión actual de PowerShell y en los procesos que se lancen desde ella. Al cerrar la terminal, desaparece.

## Quitar una variable temporal

```powershell
Remove-Item Env:MY_APP_MODE
```

## Ver dónde está instalado un programa

```powershell
Get-Command git
Get-Command node
Get-Command python
where.exe git
where.exe node
```

Si `git` funciona en una terminal pero no en otra, cierra y vuelve a abrir VS Code/Windows Terminal para recargar PATH.

### ¿Qué es PATH?

`PATH` es una variable que contiene carpetas de programas. Cuando escribes `git`, Windows busca `git.exe` dentro de esas carpetas. Si un programa está instalado pero no se reconoce, puede que su carpeta no esté en PATH o que la terminal no se haya reiniciado.

### Seguridad con secretos

No guardes API keys, contraseñas ni tokens directamente en comandos que vayas a compartir, capturas, repositorios o archivos públicos. Para proyectos locales se suelen usar archivos `.env`, que deben estar incluidos en `.gitignore`. En producción se usan los mecanismos de secretos del proveedor de hosting o CI/CD.

---

# 10. Node.js, npm y proyectos JavaScript

Estos comandos se aplican si tu proyecto usa Node.js (por ejemplo, React, Next.js, Vite, Express o herramientas de frontend).

## Comprobar instalación

```powershell
node --version
npm --version
```

Si aparece “command not found” o “not recognized”, instala Node.js desde el sitio oficial o mediante un gestor de versiones confiable y reinicia la terminal.

## Crear un proyecto npm

```powershell
mkdir my-node-project
cd my-node-project
npm init -y
```

`npm init -y` crea un `package.json` con valores predeterminados.

## Instalar dependencias

```powershell
npm install
npm install express
npm install -D vite
npm uninstall express
```

- `npm install`: instala las dependencias declaradas en `package.json` y usa el lockfile si está disponible.
- `npm install paquete`: agrega un paquete al proyecto.
- `-D`: instala una dependencia de desarrollo.
- `npm uninstall`: elimina un paquete del proyecto.

## Ejecutar scripts del proyecto

```powershell
npm run
npm run dev
npm run build
npm run test
npm start
```

Los scripts disponibles dependen de `package.json`. Usa `npm run` para ver la lista. `dev`, `build`, `test` y `start` no existen automáticamente: el proyecto debe declararlos.

## `npm install` vs. `npm ci`

- `npm install`: instala/actualiza dependencias y puede modificar `package-lock.json`.
- `npm ci`: instalación limpia y reproducible basada en `package-lock.json`; elimina primero `node_modules` y requiere que el lockfile coincida con `package.json`.

En proyectos de equipo o CI, `npm ci` es habitual para instalaciones reproducibles. No lo uses si no tienes un `package-lock.json` válido.

## Ejecutar herramientas sin instalación global

```powershell
npx vite --version
npx create-vite@latest
```

`npx` puede ejecutar herramientas del proyecto o descargar temporalmente un paquete. Revisa el nombre y la procedencia del paquete antes de ejecutarlo.

## Archivos importantes de Node

| Archivo/carpeta | Qué contiene | ¿Se suele subir a Git? |
|---|---|---|
| `package.json` | Datos, scripts y dependencias | Sí |
| `package-lock.json` | Versiones resueltas de dependencias | Sí |
| `node_modules/` | Paquetes instalados | No |
| `.env` | Configuración y posibles secretos | No |
| `.env.example` | Plantilla sin secretos | Sí, si no contiene secretos |

---

# 11. Python y entornos virtuales

## Comprobar instalación

En Windows suele funcionar el launcher `py`:

```powershell
py --version
python --version
py -0p
```

`py -0p` muestra las instalaciones de Python conocidas por el launcher, si está disponible.

## Crear un proyecto y un entorno virtual

```powershell
mkdir python-project
cd python-project
py -m venv .venv
```

Un **entorno virtual** mantiene las librerías de ese proyecto separadas de las de otros proyectos.

## Activar el entorno en PowerShell

```powershell
.\.venv\Scripts\Activate.ps1
```

Si PowerShell bloquea el script por la política de ejecución, no cambies la política global sin entender el efecto. Una opción limitada a la sesión actual es:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

Cierra esa terminal para que el alcance `Process` deje de aplicarse. Sigue las políticas de seguridad de tu equipo si es administrado por una organización.

Cuando se activa, normalmente aparece `(.venv)` al principio del prompt.

## Instalar y gestionar paquetes

```powershell
python -m pip install --upgrade pip
python -m pip install requests
python -m pip list
python -m pip show requests
python -m pip uninstall requests
```

Prefiere `python -m pip` para asegurarte de que `pip` pertenece al intérprete de Python que estás usando.

## Guardar las dependencias

```powershell
python -m pip freeze > requirements.txt
```

Reinstalarlas en otro equipo:

```powershell
python -m pip install -r requirements.txt
```

## Ejecutar Python

```powershell
python main.py
py main.py
python -m http.server 8000
```

El último comando levanta un servidor HTTP simple para probar archivos estáticos en el directorio actual. No lo expongas a redes públicas sin entender sus implicaciones.

## Salir del entorno virtual

```powershell
deactivate
```

## Qué guardar en Git

Normalmente sí: código, `requirements.txt`, README y archivos de configuración no sensibles.

Normalmente no: `.venv/`, `__pycache__/`, `.env`, credenciales y archivos temporales.

---

# 12. Git y GitHub desde la terminal

Git se usa para controlar versiones. GitHub aloja repositorios Git y permite colaborar.

## Comandos esenciales

```powershell
git status
git add .
git commit -m "Describe the change"
git push
git pull
git log --oneline --graph --decorate -10
```

### Rutina normal

```powershell
# 1. Confirmar que estás en el proyecto correcto
pwd

# 2. Revisar qué cambió
git status

# 3. Preparar los cambios
git add .

# 4. Revisar lo que se va a incluir
git diff --cached

# 5. Crear una versión local
git commit -m "Add contact page"

# 6. Subirla a GitHub
git push
```

### Obtener cambios remotos

```powershell
git pull
```

`git pull` trae cambios desde la rama remota que sigue tu rama actual e intenta integrarlos. Si estás trabajando con otras personas, revisa el estado antes de hacer cambios.

### Ver ramas y cambiar de rama

```powershell
git branch
 git branch -a
git switch main
git switch -c feature/contact-form
```

- `main`: rama principal habitual.
- `feature/contact-form`: ejemplo de rama de trabajo.
- `git switch -c`: crea una rama y cambia a ella.

### Configurar el repositorio remoto

```powershell
git remote -v
git remote add origin https://github.com/USER/REPOSITORY.git
git remote set-url origin https://github.com/USER/REPOSITORY.git
```

`origin` es solo el nombre convencional del remoto. No es una palabra especial obligatoria.

### Primera subida de una rama

```powershell
git push --set-upstream origin main
```

Esto sube `main` y configura el seguimiento de `origin/main`. En subidas posteriores normalmente basta con `git push`.

### Ver diferencias

```powershell
git diff                  # Cambios no preparados
git diff --staged         # Cambios preparados para commit
git show --stat           # Resumen del último commit
git log --oneline -10     # Últimos diez commits
```

### Deshacer con cuidado

```powershell
git restore archivo.txt               # Descarta cambios locales no preparados de ese archivo
git restore --staged archivo.txt      # Quita el archivo del staging, pero conserva los cambios
```

Estos comandos pueden descartar trabajo. Antes de usarlos, revisa `git status` y conserva una copia si no estás seguro.

**No uses `git push --force` como solución genérica**: puede sobrescribir historia remota y afectar a otras personas. Para aprender Git en profundidad, consulta tu archivo `GIT_GITHUB_CHEATSHEET.md`.

---

# 13. SSH, autenticación y conexiones remotas

SSH permite autenticarte y conectarte de forma segura a otros equipos o servicios. GitHub admite autenticación SSH para operaciones Git.

## Comprobar si ya tienes claves

```powershell
Get-ChildItem "$HOME\.ssh"
```

No compartas los archivos privados, normalmente llamados `id_ed25519` o `id_rsa`. La clave pública suele terminar en `.pub` y es la que puedes registrar en servicios compatibles.

## Crear una clave SSH Ed25519

```powershell
ssh-keygen -t ed25519 -C "tu-email@example.com"
```

Sigue las instrucciones. Es recomendable proteger la clave privada con una passphrase.

## Mostrar la clave pública

```powershell
Get-Content "$HOME\.ssh\id_ed25519.pub"
```

Copia solamente la clave pública al servicio en el que la vayas a registrar. Nunca compartas `id_ed25519` sin `.pub`.

## Probar conexión con GitHub

```powershell
ssh -T git@github.com
```

La primera conexión puede pedir confirmar la huella del servidor. Verifica la huella con la documentación oficial de GitHub antes de aceptarla.

## Cambiar el remoto HTTPS a SSH

```powershell
git remote set-url origin git@github.com:USER/REPOSITORY.git
git remote -v
```

Hazlo solo después de configurar y probar SSH.

---

# 14. Instalar herramientas y paquetes

## WinGet (gestor de paquetes de Windows)

En versiones compatibles de Windows 10/11:

```powershell
winget --version
winget search git
winget list
winget install --id Git.Git -e
winget upgrade --all
```

- `search`: buscar un paquete.
- `list`: ver programas instalados que reconoce WinGet.
- `install`: instalar un paquete.
- `upgrade --all`: actualizar paquetes disponibles. Revisa qué se actualizará antes de aceptar.

## Verificar ejecutables

```powershell
Get-Command git
Get-Command code
Get-Command node
Get-Command python
where.exe git
```

## Instalar software con cuidado

- Descarga herramientas desde su web oficial o un gestor de paquetes confiable.
- Comprueba el identificador del paquete antes de instalarlo.
- Desconfía de comandos que descargan scripts desconocidos y los ejecutan inmediatamente.
- No pegues instrucciones de internet con permisos de administrador sin entenderlas.

---

# 15. Diagnóstico de errores

## “The term 'git' is not recognized”

Windows no encuentra Git.

```powershell
Get-Command git
where.exe git
```

Soluciones habituales: comprobar que Git está instalado, verificar que su directorio está en PATH y reiniciar la terminal o VS Code.

## “The system cannot find the path specified”

La ruta es incorrecta o no existe.

```powershell
Test-Path "C:\Users\Patron\Downloads\my first website"
Get-Location
```

Copia la ruta desde el Explorador y ponla entre comillas.

## “Port 3000 is already in use”

Otro proceso está usando el puerto.

```powershell
Get-NetTCPConnection -LocalPort 3000 -State Listen
```

Inspecciona el PID y detén únicamente el proceso correcto. También puedes configurar tu aplicación para usar otro puerto si el proyecto lo permite.

## “npm is not recognized”

Node.js/npm no está instalado o no está en PATH.

```powershell
Get-Command node
Get-Command npm
node --version
npm --version
```

Instala Node.js desde la fuente oficial y reinicia la terminal.

## “Execution of scripts is disabled” al activar `.venv`

PowerShell bloquea el script de activación. Para permitirlo solo durante la sesión actual:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

No cambies el alcance `LocalMachine` sin comprender la política y tener autorización.

## Un comando parece congelado

Puede estar ejecutando un proceso interactivo o esperando entrada. Lee la salida. Para interrumpir normalmente, presiona `Ctrl + C`.

## Revisar el código de salida

```powershell
$LASTEXITCODE
$?
```

Un código `0` suele indicar que un programa externo terminó correctamente. Consulta la documentación de la herramienta para interpretar otros códigos.

---

# 16. Seguridad: comandos peligrosos y hábitos profesionales

Un developer profesional no solo sabe ejecutar comandos; sabe limitar su alcance y proteger sus datos.

## Antes de borrar o sobrescribir

```powershell
Get-Location
Get-ChildItem .\target-folder
Remove-Item .\target-folder -Recurse -WhatIf
```

Confirma que:

1. Estás en la carpeta correcta.
2. La ruta seleccionada es la que querías modificar.
3. Tienes una copia o Git contiene el trabajo que necesitas conservar.
4. Entiendes si el comando sobrescribe, elimina o modifica archivos.

## No ejecutes a ciegas

Ten especial cuidado con:

- `Remove-Item -Recurse` y `Remove-Item -Force`.
- Comandos que usan `-Force` o permisos de administrador.
- Scripts descargados de internet.
- Comandos que modifican PATH o políticas de ejecución.
- Comandos Git que reescriben historia, como `reset --hard` y `push --force`.
- Comandos que borran bases de datos, recursos cloud o contenedores.

## Protege secretos

Un `.gitignore` típico para proyectos web/Python puede incluir:

```gitignore
# Secrets / environment files
.env
.env.*
!.env.example

# Node
node_modules/

# Python
.venv/
venv/
__pycache__/
*.py[cod]

# Build output
 dist/
build/
.next/

# Logs
*.log

# OS / editor
.DS_Store
Thumbs.db
.vscode/
```

Adapta el archivo a tu proyecto. No ignores archivos de configuración que tu equipo necesite compartir sin revisar primero.

**Importante:** si una clave secreta ya fue subida a GitHub, borrar el archivo en un commit posterior no garantiza que el secreto desaparezca del historial. Revoca o rota la clave inmediatamente y sigue el procedimiento del proveedor.

## Usa privilegios mínimos

No ejecutes VS Code o PowerShell como administrador de manera habitual. Usa permisos elevados solo cuando una tarea los requiera y entiendas por qué.

---

# 17. VS Code: terminal y productividad

## Abrir VS Code desde la terminal

Si el comando `code` está disponible:

```powershell
code .                         # Abre la carpeta actual
code .\index.html              # Abre un archivo concreto
code -n .                      # Abre una ventana nueva
```

Si `code` no se reconoce, abre VS Code desde el menú Inicio o habilita el comando de VS Code para la terminal según la documentación de tu instalación.

## Abrir una terminal en VS Code

- Menú: **Terminal → New Terminal**.
- Atajo predeterminado habitual: `Ctrl + Shift + ` (acento grave; puede variar según teclado y configuración).
- Verifica el perfil: PowerShell, Command Prompt o Git Bash.

## Múltiples terminales

Puedes usar terminales separadas para tareas distintas:

- Terminal 1: `npm run dev`.
- Terminal 2: comandos Git.
- Terminal 3: scripts de Python, pruebas o herramientas.

No cierres una terminal si está ejecutando un servidor que necesitas. Para detenerlo de forma normal, usa `Ctrl + C`.

---

# 18. Atajos de teclado

| Atajo | Acción habitual |
|---|---|
| `Tab` | Autocompletar comandos y rutas |
| `↑` / `↓` | Navegar por el historial de comandos |
| `Ctrl + C` | Interrumpir el comando o proceso actual |
| `Ctrl + L` | Limpiar la pantalla en muchas shells; `clear` también funciona en PowerShell |
| `Ctrl + R` | Buscar en el historial en algunas shells; el comportamiento depende del perfil/extensiones |
| `Home` | Ir al inicio de la línea |
| `End` | Ir al final de la línea |
| `Ctrl + ←` / `Ctrl + →` | Moverse por palabras en muchos perfiles |
| `F7` | Ver historial de comandos en Windows PowerShell clásico |

Los atajos pueden variar según Windows Terminal, VS Code, versión de PowerShell y configuración del teclado.

---

# 19. Flujos de trabajo reales

## A. Abrir un proyecto existente

```powershell
cd "C:\Users\Patron\Downloads\my first website"
pwd
ls
code .
```

## B. Crear una carpeta para un proyecto nuevo

```powershell
cd "$HOME\Documents"
mkdir Projects
cd .\Projects
mkdir my-new-app
cd .\my-new-app
code .
```

## C. Empezar una app Node/Vite (si Node está instalado)

```powershell
npm create vite@latest
```

Sigue las preguntas del asistente, entra en la carpeta creada y luego:

```powershell
cd .\NOMBRE-DEL-PROYECTO
npm install
npm run dev
```

El nombre del script y el puerto dependen de la plantilla. Abre en el navegador la dirección local que aparece en la terminal.

## D. Ejecutar un proyecto Python

```powershell
cd "C:\Users\Patron\Documents\python-project"
.\.venv\Scripts\Activate.ps1
python main.py
```

Si el entorno no existe todavía, créalo con `py -m venv .venv` y luego actívalo.

## E. Revisar el proyecto antes de subir cambios

```powershell
pwd
ls
git status
git diff
git diff --cached
```

Revisa que no vayas a incluir `.env`, claves, archivos personales, `node_modules` o `.venv`.

## F. Guardar y subir cambios a GitHub

```powershell
git add .
git status
git diff --cached
git commit -m "Describe what changed"
git push
```

## G. Descargar el proyecto en otra computadora

```powershell
cd "$HOME\Documents\Projects"
git clone https://github.com/USER/REPOSITORY.git
cd .\REPOSITORY
code .
```

Luego instala las dependencias indicadas por el proyecto, por ejemplo `npm ci` o crea el entorno virtual de Python.

## H. Investigar un problema

```powershell
pwd
Get-Command nombre-del-programa
nombre-del-programa --version
Get-Help nombre-del-comando -Examples
```

Después copia el mensaje de error completo y busca la frase exacta. No ejecutes una solución antes de entender qué modifica.

---

# 20. Comandos de Linux/macOS: equivalencias rápidas

Si en el futuro usas Linux, macOS o Git Bash, encontrarás nombres diferentes. Esta tabla muestra equivalencias habituales:

| Tarea | PowerShell | Bash (Linux/macOS) |
|---|---|---|
| Ubicación actual | `Get-Location` / `pwd` | `pwd` |
| Listar archivos | `Get-ChildItem` / `ls` | `ls` |
| Cambiar carpeta | `Set-Location` / `cd` | `cd` |
| Crear carpeta | `New-Item -ItemType Directory` / `mkdir` | `mkdir` |
| Copiar | `Copy-Item` / `cp` | `cp` |
| Mover/renombrar | `Move-Item` / `mv` | `mv` |
| Borrar | `Remove-Item` / `rm` | `rm` |
| Mostrar archivo | `Get-Content` / `cat` | `cat` |
| Buscar texto | `Select-String` | `grep` |
| Limpiar pantalla | `Clear-Host` / `clear` | `clear` |
| Ver procesos | `Get-Process` | `ps`, `top` |
| Variables de entorno | `$env:NAME` | `$NAME` |

**Advertencia:** que un alias exista en PowerShell no significa que tenga exactamente el mismo comportamiento que el comando Unix equivalente. En particular, opciones de `rm`, `cp`, `mv` y `curl` pueden diferir.

En Windows PowerShell, `curl` puede ser un alias de `Invoke-WebRequest`. Para invocar el ejecutable curl real, utiliza `curl.exe`.

---

# 21. Glosario

| Término | Explicación |
|---|---|
| CLI | Command Line Interface: interfaz de línea de comandos |
| Shell | Programa que interpreta los comandos |
| Terminal | Aplicación donde utilizas una shell |
| Path | Ruta de un archivo o carpeta; también nombre de una variable del sistema |
| Working directory | Carpeta desde la que se ejecuta el comando |
| Argument | Valor que se entrega a un comando |
| Parameter/flag | Opción que modifica el comportamiento de un comando |
| Environment variable | Valor de configuración disponible para procesos |
| PATH | Variable que indica dónde buscar ejecutables |
| Process | Programa que está ejecutándose |
| PID | Identificador de un proceso |
| Port | Punto lógico de comunicación de red, por ejemplo 3000 o 8000 |
| Package manager | Herramienta que instala y gestiona paquetes, como npm o pip |
| Dependency | Librería o paquete que necesita un proyecto |
| Runtime | Entorno que ejecuta un programa, como Node.js o Python |
| Virtual environment | Entorno aislado para dependencias de Python |
| Repository | Proyecto cuyo historial se gestiona con Git |
| Script | Archivo o instrucción que automatiza tareas |
| Exit code | Número que informa cómo terminó un programa |
| stdout | Salida estándar de un programa |
| stderr | Salida estándar de errores |
| stdin | Entrada estándar de un programa |

---

# 22. Plan para practicar

La mejor manera de aprender la terminal es utilizarla en tareas pequeñas y reales. Practica en una carpeta de prueba, no en carpetas del sistema.

## Nivel 1 — Navegación

- [ ] Ejecuta `pwd` y explica qué muestra.
- [ ] Ejecuta `ls` y reconoce archivos y carpetas.
- [ ] Entra en una carpeta con `cd`.
- [ ] Sube un nivel con `cd ..`.
- [ ] Practica una ruta con espacios y comillas.

## Nivel 2 — Archivos

- [ ] Crea una carpeta `terminal-practice`.
- [ ] Crea `notes.txt`.
- [ ] Escribe contenido con `Set-Content`.
- [ ] Léelo con `Get-Content`.
- [ ] Cópialo y cámbiale el nombre.
- [ ] Prueba `Remove-Item -WhatIf` antes de borrar una copia.

Ejemplo de práctica:

```powershell
mkdir terminal-practice
cd .\terminal-practice
Set-Content .\notes.txt "Learning PowerShell"
Get-Content .\notes.txt
Copy-Item .\notes.txt .\notes-backup.txt
Rename-Item .\notes-backup.txt backup.txt
```

## Nivel 3 — Desarrollo

- [ ] Comprueba `node --version` y `npm --version` si usas JavaScript.
- [ ] Comprueba `py --version` si usas Python.
- [ ] Inicia un proyecto y ejecútalo desde la terminal.
- [ ] Detén el servidor con `Ctrl + C`.
- [ ] Investiga qué proceso usa un puerto.

## Nivel 4 — Flujo profesional

- [ ] Abre un proyecto con `code .`.
- [ ] Usa dos terminales para tareas distintas.
- [ ] Ejecuta Git desde la carpeta del proyecto.
- [ ] Revisa `git status` y `git diff` antes de hacer commit.
- [ ] Guarda un cambio con un mensaje de commit claro.
- [ ] Sube el cambio a GitHub.

---

# 23. Checklist de consulta rápida

Antes de ejecutar comandos:

- [ ] ¿Estoy en la carpeta correcta? (`pwd`)
- [ ] ¿Sé qué archivos contiene? (`ls`)
- [ ] ¿Entiendo qué hace el comando y sus opciones?
- [ ] ¿La ruta con espacios está entre comillas?
- [ ] ¿El comando puede borrar, sobrescribir o publicar algo?
- [ ] ¿Estoy exponiendo claves, tokens o datos privados?

Al trabajar en una app:

- [ ] ¿Instalé las dependencias correctas?
- [ ] ¿Estoy usando el entorno virtual o runtime adecuado?
- [ ] ¿Sé qué terminal está ejecutando el servidor?
- [ ] ¿Sé cómo detenerlo (`Ctrl + C`)?
- [ ] ¿Revisé el mensaje de error completo?

Antes de subir código:

- [ ] ¿Estoy en el repositorio correcto?
- [ ] ¿Revisé `git status`?
- [ ] ¿Revisé los cambios que voy a incluir?
- [ ] ¿Excluí `.env`, secretos y dependencias generadas?
- [ ] ¿El commit explica el cambio?

---

## Documentación oficial para profundizar

- PowerShell: https://learn.microsoft.com/powershell/
- PowerShell reference: https://learn.microsoft.com/powershell/module/microsoft.powershell.core/
- Windows Terminal: https://learn.microsoft.com/windows/terminal/
- VS Code terminal: https://code.visualstudio.com/docs/terminal/basics
- Git: https://git-scm.com/doc
- GitHub Docs: https://docs.github.com/
- Node.js: https://nodejs.org/en/learn
- npm CLI: https://docs.npmjs.com/cli/
- Python: https://docs.python.org/3/
- Python `venv`: https://docs.python.org/3/library/venv.html

---

**Regla final:** no memorices comandos como si fueran fórmulas. Aprende qué problema resuelve cada uno, qué archivos o procesos afecta y cómo comprobar el resultado. Esa es la diferencia entre simplemente escribir comandos y utilizar la terminal con criterio profesional.
