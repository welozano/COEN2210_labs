# Lab 1 — Introducción a Git y GitHub desde la Consola
## COEN 2210 — Introduction to Programming

**Duración:** 2 horas
**Requisitos:** Ninguno — no se usará ningún IDE en este laboratorio, solo la terminal/consola.

> 💻 **¿Primera vez usando la terminal/consola?** Este laboratorio asume que sabes lo básico para moverte entre carpetas (`cd`) y listar archivos (`ls`/`dir`). Si no te sientes cómodo con eso todavía, completa primero el [**Tutorial Básico de Terminal**](../Tutorial_Basico_Terminal.md) — está pensado para hacerse en casa, antes de esta sesión.

---

## Objetivos

Al finalizar este laboratorio, el estudiante podrá:
1. Explicar la diferencia entre Git y GitHub.
2. Configurar Git en una máquina nueva.
3. Crear una cuenta de GitHub.
4. Ejecutar el flujo básico de trabajo: `init`, `add`, `commit`, `push`, `clone`.
5. Conectar un repositorio local con un repositorio remoto en GitHub.

---

## Parte 0 — Git vs. GitHub (5 min)

- **Git** es el programa que corre en tu computadora y lleva el historial de cambios de tus archivos (control de versiones).
- **GitHub** es un servicio en línea donde puedes **guardar una copia remota** de tus repositorios de Git, compartirlos, y colaborar con otras personas.

Analogía: Git es como el "guardar" con historial de tu proyecto; GitHub es como el Google Drive donde subes esa copia para no perderla y compartirla.

---

## Parte 1 — Instalar y verificar Git (10 min)

Las computadoras del laboratorio **no tienen Git instalado** — lo vamos a instalar juntos como primer paso.

### Windows — instalación por consola (método preferido)

> 💻 **Vas a usar la terminal.** Abre **PowerShell** o **cmd** (busca "PowerShell" en el menú de inicio) y escribe el siguiente comando exactamente como aparece, luego presiona `Enter`:

```powershell
winget install --id Git.Git -e --source winget
```

**¿Qué hace este comando?** `winget` es el manejador de paquetes de Windows — descarga e instala Git directamente desde la terminal, sin necesidad de abrir un navegador ni ejecutar un instalador manualmente.

**Qué deberías ver:** una barra de progreso de descarga, seguida de un mensaje de instalación exitosa. Puede tardar 1-3 minutos dependiendo de la red.

**Después de instalar:** cierra la ventana de la terminal por completo y ábrela de nuevo. Esto es necesario para que Windows reconozca el nuevo comando `git` — si no cierras y abres de nuevo, el siguiente paso (`git --version`) va a fallar aunque la instalación haya sido exitosa.

> **Alternativa (si `winget` no está disponible en tu computadora):** descarga el instalador manualmente desde [git-scm.com/download/win](https://git-scm.com/download/win) y sigue el asistente de instalación — las opciones por defecto funcionan bien, no es necesario cambiar nada.

### Mac — alternativa

> 💻 **Vas a usar la terminal.** Abre la app **Terminal** (búscala con Spotlight: `Cmd + Espacio`, escribe "Terminal").

Al correr el comando de verificación (`git --version`, abajo) por primera vez, macOS normalmente te muestra una ventana ofreciendo instalar las **"Command Line Developer Tools"** automáticamente — dale clic a **Install** y espera a que termine (puede tardar varios minutos).

> **Alternativa:** `brew install git` si ya tienes Homebrew instalado.

### Linux — alternativa

Usa el manejador de paquetes de tu distribución, por ejemplo `sudo apt install git` (Ubuntu/Debian) o `sudo dnf install git` (Fedora).

### Verificar la instalación

Independientemente del método usado, confirma que quedó instalado escribiendo en la terminal:

```bash
git --version
```

**Qué deberías ver:** algo como `git version 2.4x.x` (el número exacto no importa, solo que aparezca una versión). Si no aparece nada o da error, avisa al profesor/asistente antes de continuar — no sigas al siguiente paso sin esto funcionando.

---

## Parte 2 — Configurar tu identidad en Git (5 min)

Git necesita saber quién eres para registrar tus cambios correctamente. Es recomendable que uses el mismo correo electrónico que vas a usar para crear tu cuenta de GitHub en la Parte 3 — así tus commits van a quedar vinculados a tu perfil correctamente.

Esto se configura **una sola vez por computadora**:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu_correo@ejemplo.com"
```

**¿Qué hace esto?** Guarda tu nombre y correo en la configuración global de Git en esa computadora — cada commit que hagas de ahora en adelante va a quedar "firmado" con esta información.

Verifica que quedó bien configurado:

```bash
git config --global --list
```

**Qué deberías ver:** una lista con `user.name=Tu Nombre` y `user.email=tu_correo@ejemplo.com` entre otras líneas.

---

## Parte 3 — Crear tu cuenta de GitHub (10 min)

1. Ve a [https://github.com/signup](https://github.com/signup)
2. Regístrate con tu correo institucional o personal — **usa el mismo correo que configuraste en la Parte 2**.
3. Elige un **username** profesional (lo vas a usar el resto de la carrera — evita apodos raros).
4. Verifica tu correo.

Guarda tu usuario de GitHub — lo necesitarás en el resto del curso.

---

## Parte 4 — Tu primer repositorio local (15 min)

Vamos a crear una carpeta de proyecto y convertirla en un repositorio Git.

1. Primero, identifica o crea un folder en tu computadora donde vas a guardar todos los repositorios relacionados a esta clase durante el semestre. Puedes darle un nombre como `COEN2210_intro_to_programming`.
2. Navega hasta ese folder usando la terminal. Ahí vamos a crear una carpeta nueva específica para este laboratorio.

> 💻 **Vas a usar la terminal.** Escribe estos tres comandos, uno a la vez, presionando `Enter` después de cada uno:

```bash
mkdir lab1-git
cd lab1-git
git init
```

**¿Qué hace cada comando?**
- `mkdir lab1-git` — crea una carpeta nueva llamada `lab1-git`.
- `cd lab1-git` — te mueve *dentro* de esa carpeta (de ahora en adelante, todo lo que hagas en la terminal ocurre ahí).
- `git init` — convierte esa carpeta en un repositorio Git (crea una carpeta oculta `.git` que va a guardar todo el historial de cambios).

**Qué deberías ver:** después de `git init`, un mensaje como `Initialized empty Git repository in .../lab1-git/.git/`.

Verifica el estado del repositorio:

```bash
git status
```

**Qué deberías ver:** un mensaje indicando que no hay commits todavía y que no hay nada para agregar (rama `main` o `master` vacía).

Ahora crea un archivo simple:

```bash
echo "Mi primer archivo en Git" > notas.txt
```

**¿Qué hace esto?** Crea un archivo de texto llamado `notas.txt` con esa línea de contenido.

Vuelve a correr `git status` — ahora Git debería mostrar `notas.txt` en rojo, bajo la sección **"Untracked files"** (archivos no rastreados) — esto significa que Git ve el archivo, pero todavía no lo está siguiendo.

---

## Parte 5 — El flujo básico: add → commit (15 min)

```bash
git add notas.txt
git status
git commit -m "Primer commit: agrego notas.txt"
```

**¿Qué hace cada comando y qué deberías ver?**
- `git add notas.txt` — le dice a Git "quiero incluir este archivo en el próximo guardado" (esto se llama *staging*). No produce ningún mensaje en pantalla.
- `git status` (de nuevo) — ahora `notas.txt` debería aparecer en **verde**, bajo "Changes to be committed" — confirma que quedó correctamente marcado para el commit.
- `git commit -m "mensaje"` — guarda ese cambio permanentemente en el historial. Deberías ver un mensaje con el número de archivos modificados y las líneas agregadas.

Revisa el historial:

```bash
git log
```

**Qué deberías ver:** el commit que acabas de hacer, con tu nombre, correo, fecha, y el mensaje que escribiste.

**Ejercicio rápido:** modifica `notas.txt` (agrega una línea nueva con un editor de texto o repitiendo el comando `echo` con `>>` en vez de `>` para no sobrescribir), y repite `add` + `commit` con un mensaje distinto. Corre `git log` de nuevo — deberías ver **dos** commits listados, el más reciente arriba.

---

## Parte 6 — Conectar tu repositorio local con GitHub (20 min)

1. En GitHub, haz clic en **New repository** (botón verde, o el ícono `+` arriba a la derecha).
2. Nombra el repositorio `lab1-git` (mismo nombre que tu carpeta local, por claridad).
3. **No** marques "Add a README" — ya tienes un repo local con contenido, marcar esa opción causaría un conflicto entre tu historial local y el de GitHub.
4. Haz clic en **Create repository**.
5. GitHub te va a mostrar un bloque de comandos bajo *"…or push an existing repository from the command line"*. Se ve parecido a esto:

> 💻 **Vas a usar la terminal.** Estos comandos van dentro de la carpeta `lab1-git` (asegúrate de estar ahí — si no sabes, escribe `pwd` en Mac/Linux o `cd` solo en Windows para ver dónde estás parado).

```bash
git remote add origin https://github.com/TU-USUARIO/lab1-git.git
git branch -M main
git push -u origin main
```

**¿Qué hace cada comando?**
- `git remote add origin <url>` — le dice a tu repositorio local "tu copia remota vive en esta dirección de GitHub". No produce mensaje en pantalla.
- `git branch -M main` — renombra tu rama principal a `main` (el estándar actual de GitHub).
- `git push -u origin main` — sube todos tus commits locales a GitHub, y además recuerda esa conexión para que en el futuro solo necesites escribir `git push` a secas.

> **Autenticación:** GitHub ya no acepta tu contraseña normal para `git push` desde consola. El método depende de tu sistema operativo:
>
> - **Windows:** Git te muestra un enlace y un código de 8 caracteres directamente en la terminal. Visita ese enlace en tu navegador, inicia sesión en GitHub, y escribe el código para autorizar. Después de la primera vez, tu computadora queda autenticada y no te lo vuelve a pedir.
> - **Mac:** este método no funciona igual por defecto en macOS. Antes de hacer `git push` por primera vez, instala el **Git Credential Manager**:
>
>   ```bash
>   brew install --cask git-credential-manager
>   ```
>
>   *(Requiere tener Homebrew instalado.)* Si no lo tienes, instálalo primero con:
>
>   ```bash
>   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
>   ```
>
>   Al final de la instalación, la terminal te va a mostrar 1-2 líneas de comando bajo "Next steps" — cópialas y pégalas tal cual para que el sistema reconozca el comando `brew`. En la mayoría de los casos (Macs con macOS Catalina en adelante, shell **zsh** por defecto) se ve así:
>
>   ```bash
>   echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
>   eval "$(/opt/homebrew/bin/brew shellenv)"
>   ```
>
>   *(Si tu terminal usa **bash** en vez de zsh, cambia `~/.zprofile` por `~/.bash_profile` en esa línea — pero usa exactamente lo que el instalador de Homebrew te muestre en pantalla, ya que puede variar según el tipo de Mac.)*
>
>   ⏱️ **Nota de tiempo:** instalar Homebrew puede tardar varios minutos, especialmente si el sistema también necesita descargar las "Command Line Developer Tools" de Apple (puede ser una descarga pesada). Si tienes varios estudiantes con Mac instalando esto al mismo tiempo en la red del lab, considera dar tiempo extra o hacerlo como paso previo antes de empezar el laboratorio formalmente.
>
>   Después de instalar Homebrew, corre `brew install --cask git-credential-manager` (arriba), cierra y vuelve a abrir la terminal. Ahora, al hacer `git push`, se va a abrir el navegador automáticamente para que inicies sesión y autorices — sin necesidad de escribir ningún código manualmente.
>
> Si te aparece algo distinto a esto, avisa al profesor/asistente para resolverlo en el momento.

**Qué deberías ver al terminar:** un mensaje con líneas como `Enumerating objects...`, `Writing objects: 100%`, y finalmente algo como `branch 'main' set up to track 'origin/main'`.

6. Refresca la página de tu repositorio en GitHub — deberías ver `notas.txt` ahí, junto con tus commits.

---

## Parte 7 — Clonar un repositorio (10 min)

`git clone` descarga una copia completa de un repositorio remoto a tu computadora — es lo que vas a usar para trabajar en el proyecto en equipo más adelante.

> 💻 **Vas a usar la terminal.** Primero sal de la carpeta actual con `cd ..`, y luego clona el repositorio:

```bash
cd ..
git clone https://github.com/TU-USUARIO/lab1-git.git lab1-git-clon
cd lab1-git-clon
ls
```

**¿Qué hace cada comando?**
- `cd ..` — te mueve un nivel arriba (sales de `lab1-git`).
- `git clone <url> lab1-git-clon` — descarga una copia completa del repositorio remoto en una carpeta nueva llamada `lab1-git-clon`.
- `cd lab1-git-clon` — entras a esa nueva carpeta.
- `ls` (o `dir` en Windows si `ls` no funciona) — lista los archivos dentro.

**Qué deberías ver:** el mismo `notas.txt` que subiste antes, ahora dentro de esta carpeta nueva — confirma que la copia remota en GitHub sí tiene tu contenido.

---

## Parte 8 — Repaso de comandos (para tu referencia)

| Comando | Qué hace |
|---|---|
| `git init` | Convierte la carpeta actual en un repositorio Git |
| `git status` | Muestra el estado actual (qué cambió, qué está listo para commit) |
| `git add <archivo>` | Marca un archivo para incluirlo en el próximo commit |
| `git add -A` | Marca todos los cambios (nuevos, modificados, y eliminados) para el próximo commit |
| `git rm --cached <archivo>` | Deja de rastrear un archivo sin borrarlo de la computadora |
| `git mv <origen> <destino>` | Mueve/renombra un archivo y lo deja listo para commit en un solo paso |
| `git commit -m "mensaje"` | Guarda los cambios marcados, con un mensaje |
| `git log` | Muestra el historial de commits |
| `git remote add origin <url>` | Conecta el repo local con uno remoto en GitHub |
| `git push` | Sube tus commits al repositorio remoto |
| `git clone <url>` | Descarga una copia de un repositorio remoto |
| `git pull` | Trae los cambios más recientes del repositorio remoto |

---

## Entregable del laboratorio

Envía al profesor (por el medio indicado en clase) el enlace de tu repositorio `lab1-git` en GitHub, con al menos 3 archivos y **4 commits** visibles en el historial.

---

## Próximo laboratorio (Lab 2)

En el Lab 2 vamos a usar **Visual Studio Code** (ya instalado en las computadoras del laboratorio) para escribir y ejecutar programas en C++, y vamos a repetir este mismo flujo de Git/GitHub pero **desde dentro del IDE**, usando el panel de Control de Versiones en vez de la consola.
