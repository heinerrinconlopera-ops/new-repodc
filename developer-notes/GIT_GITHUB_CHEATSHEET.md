# Git & GitHub Cheat Sheet

Guía práctica en español para aprender Git y GitHub, trabajar desde VS Code en Windows y consultar comandos cuando los necesites.

> **Idea principal:** Git guarda el historial de cambios de tu proyecto. GitHub aloja una copia remota del repositorio para compartirlo y acceder a él desde otras computadoras. Para que tus cambios estén respaldados en GitHub, normalmente necesitas hacer **commit** y después **push**.

---

## 1. Git vs. GitHub: ¿qué hace cada uno?

| Concepto | Qué es | Para qué sirve |
|---|---|---|
| **Git** | Sistema de control de versiones | Registra cambios y permite volver a versiones anteriores. Funciona en tu computadora. |
| **GitHub** | Plataforma online que aloja repositorios Git | Guarda repositorios en la nube, facilita colaborar y revisar código. |
| **Repository (repo)** | Carpeta de proyecto administrada por Git | Contiene los archivos del proyecto y su historial. |
| **Commit** | Punto guardado en el historial | Representa un conjunto de cambios con un mensaje. |
| **Remote** | Repositorio alojado en otro lugar | Por ejemplo, la copia de tu repo en GitHub. |
| **Branch** | Línea independiente de trabajo | Permite desarrollar una función sin alterar directamente otra rama. |
| **Merge** | Integración de una rama en otra | Combina cambios de distintas líneas de trabajo. |
| **Pull request (PR)** | Solicitud para integrar cambios en GitHub | Permite revisar y discutir cambios antes de combinarlos. |

### Una forma sencilla de imaginarlo

- **Tu carpeta del proyecto:** donde editas `index.html`, `style.css`, Python, etc.
- **Git:** registra qué cambió dentro de esa carpeta.
- **Commit:** guarda una versión en el historial local.
- **GitHub:** aloja una copia remota del repositorio.
- **Push:** envía tus commits a GitHub.
- **Pull:** trae e integra cambios del repositorio remoto.

**Importante:** hacer `commit` no sube nada a GitHub. Para enviar esos commits, usa `git push`.

---

## 2. Los cuatro estados que debes entender

Git normalmente muestra los archivos en distintos estados:

1. **Untracked:** Git ve el archivo, pero todavía no lo está siguiendo.
2. **Modified:** un archivo que Git ya sigue fue modificado.
3. **Staged:** preparaste el cambio para incluirlo en el próximo commit con `git add`.
4. **Committed:** el cambio ya quedó guardado en el historial local con `git commit`.

Flujo visual:

```text
Editas archivos
     |
     v
Working directory (cambios locales)
     |
     | git add
     v
Staging area (cambios preparados)
     |
     | git commit
     v
Local repository (historial en tu PC)
     |
     | git push
     v
Remote repository (GitHub)
```

El comando que más te ayuda a saber dónde estás es:

```bash
git status
```

Úsalo antes y después de operaciones importantes.

---

## 3. Instalar y configurar Git (normalmente una sola vez por computadora)

### Comprobar que Git está instalado

```powershell
git --version
```

Ejemplo de respuesta:

```text
git version 2.56.1.windows.1
```

Si Windows dice que `git` no se reconoce, instala Git para Windows desde:

https://git-scm.com/downloads/win

Durante la instalación selecciona la opción para usar Git desde la línea de comandos y software de terceros. Después, cierra y vuelve a abrir VS Code o PowerShell.

### Configurar tu identidad

Usa tu nombre y el correo que quieres asociar con tus commits:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu-correo@example.com"
```

Ver la configuración:

```bash
git config --global --list
```

La opción `--global` aplica a todos tus repositorios de esa computadora. Puedes configurar una identidad diferente para un proyecto si lo necesitas, quitando `--global` y ejecutando el comando dentro de ese repositorio.

---

## 4. Repositorio: crear uno o descargar uno existente

Hay dos situaciones distintas. No necesitas ejecutar las dos.

### A. Ya tienes una carpeta de proyecto en tu computadora

1. Abre **esa carpeta** en VS Code: `File → Open Folder`.
2. Abre la terminal integrada: `Terminal → New Terminal`.
3. Comprueba la ubicación:

```powershell
pwd
```

4. Inicializa Git dentro de la carpeta del proyecto:

```bash
git init
```

5. Comprueba el estado:

```bash
git status
```

`git init` crea una carpeta oculta llamada `.git`, donde Git guarda su historial y configuración.

> **Cuidado en Windows:** no ejecutes `git init` en `C:\Users\TuUsuario` ni en una carpeta general que contenga Desktop, Documents, Downloads y otros archivos personales. Inicializa Git dentro de la carpeta específica del proyecto.

### B. El proyecto ya existe en GitHub y quieres descargarlo

Copia la URL del repositorio en GitHub y ejecuta:

```bash
git clone https://github.com/USUARIO/NOMBRE-REPO.git
```

Esto descarga el repositorio y crea una carpeta para él. Después entra en esa carpeta:

```powershell
cd NOMBRE-REPO
```

**Diferencia importante:** `git init` empieza a controlar una carpeta local; `git clone` descarga un repositorio que ya existe.

---

## 5. El workflow diario: los comandos que MÁS vas a usar

Este es el ciclo habitual cuando trabajas solo en un proyecto:

### 1. Revisar el estado

```bash
git status
```

Te dice qué archivos cambiaron, cuáles están preparados y en qué rama estás.

### 2. Preparar los cambios

```bash
git add .
```

Prepara todos los cambios detectados dentro del repositorio actual. Revisa `git status` antes de hacerlo para asegurarte de no incluir archivos que no quieres guardar.

Para preparar un archivo específico:

```bash
git add index.html
```

Para preparar varios archivos:

```bash
git add index.html style.css
```

### 3. Guardar una versión (commit)

```bash
git commit -m "Add homepage layout"
```

El mensaje debe describir qué cambiaste. Algunos ejemplos:

```bash
git commit -m "Create contact page"
git commit -m "Fix navigation menu"
git commit -m "Update responsive styles"
git commit -m "Add form validation"
```

Un commit es un punto del historial local. No es todavía una subida a GitHub.

### 4. Subir los commits a GitHub

```bash
git push
```

Envía los commits locales a la rama remota configurada.

### 5. Descargar cambios de GitHub

```bash
git pull
```

Descarga e integra cambios remotos en tu rama actual. Antes de trabajar en equipo o desde otra computadora, suele ser buena idea ejecutar `git pull` para comenzar con la versión más reciente.

### El ciclo para memorizar

```bash
git status
git add .
git commit -m "Describe your changes"
git push
```

**Regla mental:** `add` prepara → `commit` guarda localmente → `push` sube a GitHub.

---

## 6. ¿Qué es `main`? ¿Qué es una branch?

### Branch (rama)

Una **branch** es una línea de trabajo independiente dentro del mismo repositorio. Te permite desarrollar una función, corregir un error o experimentar sin cambiar directamente la rama principal.

Ejemplo:

```text
main
 |
 |--------------------------- (versión principal estable)
        \
         feature/contact-form  (trabajo de una función)
```

Piensa en `main` como la línea principal del proyecto y en una rama `feature/...` como un espacio separado para trabajar en una mejora.

### ¿Qué es `main`?

`main` es el nombre que se usa habitualmente para la rama principal de un repositorio. No es un comando especial ni un tipo diferente de rama: es simplemente el nombre de una rama. En repositorios antiguos puedes encontrar `master`; técnicamente ambas son ramas normales y el nombre se puede cambiar.

### Ver las ramas

```bash
git branch
```

La rama actual aparece marcada con `*`.

Ver ramas locales y remotas:

```bash
git branch -a
```

### Crear y cambiar de rama

Crear una rama nueva y cambiarte a ella en un solo paso:

```bash
git switch -c feature/contact-form
```

Cambiar a una rama que ya existe:

```bash
git switch main
```

También puedes usar el comando histórico `git checkout`, pero `git switch` es más claro para cambiar ramas.

### Subir una rama nueva a GitHub

```bash
git push -u origin feature/contact-form
```

`-u` configura el seguimiento entre tu rama local y la rama remota. Normalmente solo lo necesitas en la primera subida de esa rama; después basta con `git push`.

### Integrar una rama en `main`

Primero cambia a `main`:

```bash
git switch main
```

Trae los cambios más recientes de `main`:

```bash
git pull
```

Integra la rama de la función:

```bash
git merge feature/contact-form
```

Sube el resultado:

```bash
git push
```

Cuando ya no necesites la rama, puedes borrarla localmente:

```bash
git branch -d feature/contact-form
```

Y borrar la rama remota de GitHub:

```bash
git push origin --delete feature/contact-form
```

No borres una rama hasta confirmar que sus cambios importantes ya se integraron.

### Flujo de ramas típico

```bash
# Partir de main actualizado
git switch main
git pull

# Crear una rama para una tarea
git switch -c feature/new-navbar

# Trabajar y guardar cambios
git add .
git commit -m "Build new navigation bar"

# Publicar la rama
git push -u origin feature/new-navbar
```

Luego puedes crear un **Pull Request** en GitHub para revisar e integrar esa rama en `main`.

---

## 7. Conectar tu carpeta local con un repositorio de GitHub

En Git, la dirección de un repositorio remoto se guarda con un nombre corto. El nombre más común es **`origin`**.

### Ver los remotos configurados

```bash
git remote -v
```

Si ves algo como esto, ya tienes un remoto:

```text
origin  https://github.com/USUARIO/NOMBRE-REPO.git (fetch)
origin  https://github.com/USUARIO/NOMBRE-REPO.git (push)
```

### Agregar un remoto cuando todavía no existe

```bash
git remote add origin https://github.com/USUARIO/NOMBRE-REPO.git
```

### Cambiar la URL de `origin` si apunta al repositorio equivocado

```bash
git remote set-url origin https://github.com/USUARIO/NUEVO-REPO.git
```

### Cambiar el nombre de la rama actual a `main`

```bash
git branch -M main
```

### Primera subida de `main`

```bash
git push -u origin main
```

- `push`: envía commits.
- `origin`: nombre del remoto.
- `main`: rama que quieres enviar.
- `-u`: configura el seguimiento para que futuras subidas puedan hacerse con `git push`.

### Consejo para evitar el error `fetch first`

Si ya tienes un proyecto local y quieres subirlo a un repositorio nuevo, crea el repositorio de GitHub **vacío**, sin marcar las opciones de crear README, `.gitignore` o licencia. Luego conecta el remoto y haz el primer `push`.

Si GitHub ya tiene un README u otros commits, el historial remoto puede ser distinto del local. En ese caso hay que integrar los historiales antes de subir; no uses `push --force` como solución automática.

---

## 8. `fetch`, `pull` y `push`: diferencias

| Comando | Qué hace | Cuándo usarlo |
|---|---|---|
| `git fetch` | Descarga información y commits del remoto, pero no integra esos cambios en tu rama actual | Para revisar qué cambió en GitHub antes de integrarlo. |
| `git pull` | Hace fetch y luego integra los cambios en tu rama actual (normalmente mediante merge o la estrategia configurada) | Para actualizar tu rama local. |
| `git push` | Envía tus commits locales al remoto | Para publicar tus commits en GitHub. |

Ejemplo seguro para revisar primero:

```bash
git fetch origin
git status
git log --oneline --all --graph
```

Después, si estás listo para integrar los cambios de `main` remoto:

```bash
git pull origin main
```

---

## 9. Ver cambios e historial

### Ver estado

```bash
git status
```

### Ver cambios que todavía no preparaste con `git add`

```bash
git diff
```

### Ver cambios preparados para el próximo commit

```bash
git diff --staged
```

### Ver historial resumido

```bash
git log --oneline
```

### Ver historial con ramas y gráficos

```bash
git log --oneline --graph --decorate --all
```

### Ver los detalles de un commit

```bash
git show ID-DEL-COMMIT
```

### Ver solo los nombres de archivos modificados en el último commit

```bash
git show --name-only --oneline HEAD
```

`HEAD` normalmente representa el commit al que apunta tu rama actual.

---

## 10. Deshacer o corregir cambios

Lee esta sección con cuidado. Algunos comandos descartan trabajo permanentemente.

### Quité un archivo del staging por error

Si ejecutaste `git add` pero todavía no hiciste commit:

```bash
git restore --staged index.html
```

Esto quita el archivo del staging, pero conserva sus cambios en tu carpeta.

Para quitar todos los archivos del staging:

```bash
git restore --staged .
```

### Quiero descartar cambios locales de un archivo

```bash
git restore index.html
```

**Peligro:** descarta los cambios no guardados de ese archivo y recupera la versión del último commit. No lo ejecutes si quieres conservar esos cambios.

### Quiero corregir el mensaje del último commit

Si el commit todavía no se compartió con otros ni se subió a GitHub:

```bash
git commit --amend -m "Better commit message"
```

`--amend` reemplaza el último commit; no es una simple edición del historial. Evita usarlo en commits que otras personas ya descargaron.

### Quiero deshacer un commit que ya compartí

La opción más segura en una rama compartida suele ser:

```bash
git revert ID-DEL-COMMIT
```

Crea un commit nuevo que revierte los cambios del commit indicado, sin borrar el historial existente.

### Eliminar el último commit local (solo si entiendes las consecuencias)

Mantener los cambios preparados:

```bash
git reset --soft HEAD~1
```

Eliminar el commit y dejar los cambios sin preparar:

```bash
git reset HEAD~1
```

**Muy peligroso:** eliminar el commit y descartar los cambios:

```bash
git reset --hard HEAD~1
```

`--hard` puede borrar trabajo. No lo uses para solucionar errores de push ni si no tienes una copia de lo que quieres conservar.

---

## 11. Resolver conflictos de merge

Un conflicto aparece cuando Git no puede combinar automáticamente cambios que afectan la misma parte de un archivo.

Git puede mostrar algo parecido a:

```text
<<<<<<< HEAD
Tu versión local
=======
La versión que viene de la otra rama
>>>>>>> origin/main
```

Qué hacer:

1. Abre el archivo indicado por Git en VS Code.
2. Decide qué contenido debe quedar. Puedes conservar una versión o combinar ambas.
3. Elimina los marcadores `<<<<<<<`, `=======` y `>>>>>>>`.
4. Guarda el archivo.
5. Marca el conflicto como resuelto:

```bash
git add NOMBRE-DEL-ARCHIVO
```

6. Si estabas haciendo un merge, termina el merge con:

```bash
git commit
```

7. Después, si corresponde, sube el resultado:

```bash
git push
```

Para cancelar un merge que todavía está en progreso:

```bash
git merge --abort
```

Úsalo solo si quieres cancelar el merge y volver al estado anterior al intento. Si el conflicto ocurrió durante un `pull` con rebase, el comando para cancelar es `git rebase --abort`.

**No uses `git push --force` para arreglar un conflicto.** Primero resuelve e integra los cambios.

---

## 12. El archivo `.gitignore`: qué NO debe subirse

`.gitignore` le indica a Git qué archivos o carpetas no debe empezar a seguir. Es útil para evitar subir dependencias, archivos temporales, configuraciones personales y secretos.

Crea un archivo llamado exactamente `.gitignore` en la raíz del proyecto.

### Ejemplo para proyectos web y Python

```gitignore
# Secretos y variables de entorno
.env
.env.*
!.env.example

# Dependencias de Node.js
node_modules/

# Python
__pycache__/
*.py[cod]
.venv/
venv/

# Archivos de salida y compilación
dist/
build/
.next/

# Editores y sistema operativo
.vscode/
.DS_Store
Thumbs.db
*.log

# Entornos locales
.local/
```

Puedes ajustar este ejemplo a tu proyecto. No ignores automáticamente una carpeta si contiene archivos de configuración que tu equipo necesita compartir. Por ejemplo, algunos proyectos sí guardan archivos seleccionados de `.vscode`.

### Importante: `.gitignore` no elimina archivos que Git ya está siguiendo

Si un archivo ya fue agregado al repositorio, agregarlo después a `.gitignore` no lo deja de seguir automáticamente. Para dejar de seguirlo sin borrar tu copia local:

```bash
git rm --cached NOMBRE-DEL-ARCHIVO
```

Para una carpeta:

```bash
git rm -r --cached NOMBRE-DE-LA-CARPETA
```

Después guarda el cambio:

```bash
git add .gitignore
git commit -m "Add gitignore rules"
```

### Nunca subas secretos

No subas contraseñas, claves privadas, tokens de acceso, API keys, credenciales bancarias ni archivos `.env` con valores reales. Si subiste una clave por error, eliminar el archivo en un commit posterior no garantiza que el secreto desaparezca del historial. Revoca o rota la clave inmediatamente y revisa el historial y las herramientas de protección de secretos de GitHub.

Puedes subir un `.env.example` con nombres de variables y valores ficticios, por ejemplo:

```text
API_KEY=replace_with_your_key
DATABASE_URL=replace_with_your_database_url
```

---

## 13. GitHub: conceptos de la plataforma

| Elemento de GitHub | Qué significa |
|---|---|
| **Repository** | Proyecto alojado en GitHub. Puede ser público o privado. |
| **Public** | Cualquier persona puede ver el repositorio. |
| **Private** | Solo las personas autorizadas pueden verlo. |
| **README.md** | Página principal de documentación del repositorio. |
| **Pull Request (PR)** | Propuesta para integrar cambios de una rama en otra. |
| **Issue** | Tarea, error, idea o discusión relacionada con el proyecto. |
| **Actions** | Automatizaciones, por ejemplo, pruebas o despliegues al hacer push. |
| **Release** | Versión publicada de un proyecto, normalmente asociada a un tag. |
| **Fork** | Copia de un repositorio en otra cuenta de GitHub. |
| **Star** | Marca de interés o reconocimiento para un repositorio. |

### ¿Qué es un Pull Request?

Un Pull Request (PR) permite proponer que los cambios de una rama se integren en otra. Por ejemplo:

```text
feature/contact-form  --->  Pull Request  --->  main
```

En GitHub puedes revisar diferencias, dejar comentarios, ejecutar verificaciones y aceptar la integración.

---

## 14. Trabajar en dos computadoras

Supongamos que hiciste cambios en tu computadora A y ahora quieres continuar en la computadora B.

### Primera vez en la computadora B

Descarga el proyecto:

```bash
git clone https://github.com/USUARIO/NOMBRE-REPO.git
```

Abre la carpeta descargada en VS Code.

### Cada vez que empieces a trabajar en B

```bash
git pull
```

### Cuando termines en B

```bash
git status
git add .
git commit -m "Describe the changes"
git push
```

### Vuelves a la computadora A

Antes de editar, descarga lo último:

```bash
git pull
```

**Regla:** sube tus cambios al terminar una sesión y haz `pull` antes de empezar en otra computadora. No trabajes simultáneamente en el mismo proyecto sin coordinar los cambios.

GitHub almacena el repositorio y su historial; no sincroniza automáticamente cada vez que guardas un archivo en VS Code.

---

## 15. Comandos útiles adicionales

### Renombrar o mover archivos usando Git

```bash
git mv archivo-antiguo.html archivo-nuevo.html
```

### Eliminar un archivo del proyecto y del control de versiones

```bash
git rm archivo.html
```

Luego crea un commit para guardar el cambio.

### Guardar temporalmente cambios sin hacer commit (stash)

```bash
git stash
```

Recuperar el cambio más reciente:

```bash
git stash pop
```

Ver los stashes guardados:

```bash
git stash list
```

`stash` es útil para apartar temporalmente cambios no confirmados. No sustituye un commit ni una copia de seguridad.

### Crear una etiqueta para una versión

```bash
git tag v1.0.0
```

Subir esa etiqueta a GitHub:

```bash
git push origin v1.0.0
```

Las etiquetas permiten marcar versiones importantes, por ejemplo `v1.0.0` o `v2.1.0`.

### Ver ayuda de un comando

```bash
git help commit
git help branch
git help push
```

También puedes usar:

```bash
git commit --help
```

---

## 16. Errores comunes y cómo entenderlos

### `git is not recognized` / `git no se reconoce`

Windows no encuentra el programa. Instala Git for Windows, verifica que la opción para usar Git desde la línea de comandos esté habilitada y reinicia la terminal o VS Code.

### `fatal: not a git repository`

Estás en una carpeta que no pertenece a un repositorio Git. Usa `pwd` para revisar la ubicación y `cd` para entrar en la carpeta correcta.

```powershell
cd "C:\Users\TuUsuario\Downloads\mi-proyecto"
git status
```

### `nothing to commit, working tree clean`

No hay cambios nuevos que guardar en este momento. Puede significar que todo ya está guardado en un commit local.

### `Everything up-to-date`

No hay commits locales pendientes de enviar al remoto. No es un error.

### `remote origin already exists`

Ya tienes un remoto llamado `origin`. Revisa su URL:

```bash
git remote -v
```

Si apunta a la dirección equivocada:

```bash
git remote set-url origin https://github.com/USUARIO/NUEVO-REPO.git
```

### `src refspec main does not match any`

A menudo significa que todavía no tienes ningún commit o que tu rama tiene otro nombre. Revisa:

```bash
git status
git branch
```

Si todavía no hay commits:

```bash
git add .
git commit -m "Initial commit"
```

Si quieres que la rama actual se llame `main`:

```bash
git branch -M main
```

### `rejected ... (fetch first)` o `non-fast-forward`

El remoto tiene commits que tu rama local todavía no integra. No significa que debas borrar tu proyecto.

Revisa primero el estado:

```bash
git status
git fetch origin
```

Si tu objetivo es integrar el `main` remoto en tu `main` local:

```bash
git pull origin main
```

Resuelve cualquier conflicto, crea el commit de merge si Git lo requiere y luego:

```bash
git push
```

Si Git dice que los historiales no tienen un ancestro común y sabes que son los dos historiales correctos que deseas combinar, puede ser necesario:

```bash
git pull origin main --allow-unrelated-histories
```

Revisa y resuelve los conflictos antes de continuar. Esta opción no debe usarse automáticamente en todos los errores de push.

### `fatal: remote origin already exists` o URL incorrecta

Usa `git remote -v` y, si hace falta, `git remote set-url origin URL`.

### `Authentication failed`

GitHub no acepta la contraseña normal de tu cuenta para operaciones Git por HTTPS. Sigue el inicio de sesión del navegador que ofrece Git Credential Manager. Si una herramienta solicita un token, usa un Personal Access Token de GitHub con los permisos mínimos necesarios y nunca lo compartas ni lo guardes en el código.

### `CONFLICT` durante un merge o pull

Abre los archivos indicados, resuelve los marcadores de conflicto, guarda y ejecuta `git add`. Después termina el merge con `git commit` cuando Git lo solicite.

---

## 17. Seguridad y buenas prácticas

1. **Un repositorio por proyecto.** No inicialices Git en tu carpeta de usuario de Windows ni en una carpeta que contenga todos tus documentos.
2. **Usa `.gitignore`.** Excluye dependencias, archivos temporales y configuraciones locales que no deban compartirse.
3. **No subas secretos.** Nunca incluyas API keys, contraseñas, tokens o credenciales.
4. **Haz commits pequeños y claros.** Un commit debería representar un cambio lógico.
5. **Revisa antes de subir.** Ejecuta `git status` y, si es necesario, `git diff --staged` antes del commit.
6. **Haz push con frecuencia.** Un commit que solo existe en tu computadora no está respaldado en GitHub.
7. **Haz pull antes de empezar en otra computadora.** Así reduces conflictos.
8. **No uses `git push --force` como solución rápida.** Puede sobrescribir commits remotos. Si alguna vez necesitas reescribir una rama propia, aprende primero `--force-with-lease` y entiende el impacto.
9. **No confundas Git con una copia de seguridad completa.** Archivos ignorados, archivos grandes o datos externos pueden no estar en el repositorio. Mantén copias de seguridad de datos importantes.
10. **Protege `main` en proyectos compartidos.** Usa Pull Requests y revisiones para evitar cambios accidentales.

---

## 18. Ejemplo completo: primer proyecto local a un repositorio GitHub vacío

Este ejemplo supone que ya tienes una carpeta de proyecto en tu PC y creaste un repositorio vacío en GitHub.

### 1. Entrar en el proyecto

```powershell
cd "C:\Users\TuUsuario\Downloads\my first website"
pwd
```

### 2. Inicializar Git (solo si el proyecto todavía no tiene `.git`)

```bash
git init
```

### 3. Revisar y preparar archivos

```bash
git status
git add .
git status
```

### 4. Crear el primer commit

```bash
git commit -m "Initial website version"
```

### 5. Renombrar la rama principal a `main`

```bash
git branch -M main
```

### 6. Conectar GitHub (reemplaza la URL por la de tu repo)

```bash
git remote add origin https://github.com/USUARIO/NOMBRE-REPO.git
```

Si ya existe `origin`, usa `git remote set-url origin URL` en vez de agregarlo otra vez.

### 7. Subir por primera vez

```bash
git push -u origin main
```

### 8. Confirmar

Abre tu repositorio en GitHub y verifica que aparecen los archivos y el commit.

---

## 19. Mini diccionario

| Término | Explicación corta |
|---|---|
| `HEAD` | Referencia al commit actual de tu checkout; normalmente el último commit de la rama actual. |
| `origin` | Nombre convencional del remoto principal. Puede tener otro nombre. |
| `main` | Nombre convencional de la rama principal. |
| `master` | Otro nombre posible para una rama; común en repositorios antiguos. |
| `staging area` | Área donde preparas los cambios que entrarán en el próximo commit. |
| `tracked file` | Archivo que Git ya conoce y sigue. |
| `untracked file` | Archivo que existe en la carpeta, pero Git todavía no sigue. |
| `merge` | Integración de cambios de otra rama. |
| `conflict` | Situación en la que Git necesita que una persona elija cómo combinar cambios. |
| `clone` | Descargar un repositorio remoto y su historial. |
| `fetch` | Descargar información y commits del remoto sin integrarlos todavía. |
| `pull` | Descargar e integrar cambios remotos. |
| `push` | Enviar commits al remoto. |
| `PR` | Pull Request: propuesta de integración en GitHub. |

---

## 20. La chuleta de 30 segundos

### Lo que usarás la mayoría de los días

```bash
git status
git add .
git commit -m "Describe the change"
git push
```

### Antes de empezar a trabajar en un proyecto compartido o en otra computadora

```bash
git pull
```

### Crear una rama para una nueva función

```bash
git switch -c feature/name
```

### Volver a la rama principal

```bash
git switch main
```

### Ver ramas

```bash
git branch -a
```

### Ver el historial

```bash
git log --oneline --graph --all
```

### Revisar la URL de GitHub conectada

```bash
git remote -v
```

### Descargar un repo por primera vez

```bash
git clone https://github.com/USUARIO/NOMBRE-REPO.git
```

---

## Recursos oficiales para seguir aprendiendo

- Git - documentación oficial: https://git-scm.com/doc
- Git - libro gratuito *Pro Git*: https://git-scm.com/book/en/v2
- GitHub Docs: https://docs.github.com/
- GitHub Skills (tutoriales prácticos): https://skills.github.com/
- GitHub sobre autenticación: https://docs.github.com/en/authentication

**Consejo final:** no intentes memorizar todos los comandos de una vez. Aprende primero el ciclo `status → add → commit → push`, entiende bien `main` y las ramas, y consulta esta guía cuando necesites algo más avanzado.
