# Lab 1 — Introducción a Git y GitHub desde la Consola
## COEN 2210 — Introduction to Programming

**Duración:** 2 horas
**Requisitos:** Ninguno — no se usará ningún IDE en este laboratorio, solo la terminal/consola.

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

Abre **PowerShell** o **cmd** y ejecuta:

```powershell
winget install --id Git.Git -e --source winget
```

`winget` es el manejador de paquetes de Windows — instala Git directamente desde la terminal, sin necesidad de abrir un navegador ni ejecutar un instalador manualmente.

Cierra y vuelve a abrir la terminal después de instalar (necesario para que Windows reconozca el nuevo comando `git`).

> **Alternativa (si `winget` no está disponible en tu computadora):** descarga el instalador manualmente desde [git-scm.com/download/win](https://git-scm.com/download/win) y sigue el asistente de instalación — las opciones por defecto funcionan bien, no es necesario cambiar nada.

### Mac — alternativa

Al correr `git --version` por primera vez, macOS normalmente te ofrece instalar las "Command Line Developer Tools" automáticamente — acepta esa instalación. Alternativa: `brew install git` si usas Homebrew.

### Linux — alternativa

Usa el manejador de paquetes de tu distribución, por ejemplo `sudo apt install git` (Ubuntu/Debian) o `sudo dnf install git` (Fedora).

### Verificar la instalación

Independientemente del método usado, confirma que quedó instalado:

```bash
git --version
```

Deberías ver algo como `git version 2.4x.x`. Si no aparece nada, avisa al profesor/asistente antes de continuar.

---

## Parte 2 — Configurar tu identidad en Git (5 min)

Git necesita saber quién eres para registrar tus cambios correctamente. Esto se hace **una sola vez por computadora**:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu_correo@ejemplo.com"
```

Verifica que quedó bien configurado:

```bash
git config --global --list
```

> **Nota:** usa el mismo correo que vas a usar para tu cuenta de GitHub en la Parte 3.

---

## Parte 3 — Crear tu cuenta de GitHub (10 min)

1. Ve a [https://github.com/signup](https://github.com/signup)
2. Regístrate con tu correo institucional o personal.
3. Elige un **username** profesional (lo vas a usar el resto de la carrera — evita apodos raros).
4. Verifica tu correo.

Guarda tu usuario de GitHub — lo necesitarás en el resto del curso.

---

## Parte 4 — Tu primer repositorio local (15 min)

Vamos a crear una carpeta de proyecto y convertirla en un repositorio Git.

```bash
mkdir lab1-git
cd lab1-git
git init
```

`git init` convierte la carpeta actual en un repositorio Git (crea una carpeta oculta `.git` que guarda todo el historial).

Verifica el estado del repositorio:

```bash
git status
```

Crea un archivo simple:

```bash
echo "Mi primer archivo en Git" > notas.txt
```

Vuelve a correr `git status` — ahora Git debería mostrar `notas.txt` como un archivo **no rastreado** (untracked).

---

## Parte 5 — El flujo básico: add → commit (15 min)

```bash
git add notas.txt
git status
git commit -m "Primer commit: agrego notas.txt"
```

- `git add` le dice a Git "quiero incluir este archivo en el próximo guardado".
- `git commit -m "mensaje"` guarda ese cambio permanentemente en el historial, con un mensaje descriptivo.

Revisa el historial:

```bash
git log
```

**Ejercicio rápido:** modifica `notas.txt` (agrega una línea nueva), y repite `add` + `commit` con un mensaje distinto. Corre `git log` de nuevo — deberías ver dos commits.

---

## Parte 6 — Conectar tu repositorio local con GitHub (20 min)

1. En GitHub, haz clic en **New repository** (botón verde, o el ícono `+` arriba a la derecha).
2. Nombra el repositorio `lab1-git` (mismo nombre que tu carpeta local, por claridad).
3. **No** marques "Add a README" — ya tienes un repo local, esto evita conflictos.
4. Haz clic en **Create repository**.
5. GitHub te va a mostrar un bloque de comandos bajo *"…or push an existing repository from the command line"*. Se ve parecido a esto:

```bash
git remote add origin https://github.com/TU-USUARIO/lab1-git.git
git branch -M main
git push -u origin main
```

Ejecuta esos comandos en tu terminal (dentro de la carpeta `lab1-git`).

> **Autenticación:** GitHub ya no acepta tu contraseña normal para `git push` desde consola. Lo que veas depende de tu sistema operativo y de cómo esté configurado Git en esa computadora — no todos van a ver exactamente lo mismo. Las opciones más comunes son:
>
> - **Código de un solo uso por navegador (recomendado / más común en Windows):** Git te muestra un enlace y un código de 8 caracteres. Visitas el enlace en tu navegador, inicias sesión en GitHub, y escribes ese código para autorizar. Después de la primera vez, tu computadora queda autenticada y no te lo vuelve a pedir.
> - **Personal Access Token:** si Git te pide directamente un usuario/contraseña en la terminal, la "contraseña" debe ser un Personal Access Token generado desde tu cuenta de GitHub, no tu contraseña real.
>
> Si te aparece algo distinto a estas dos opciones, o no te aparece nada, avisa al profesor/asistente para resolverlo en el momento.

6. Refresca la página de tu repositorio en GitHub — deberías ver `notas.txt` ahí.

---

## Parte 7 — Clonar un repositorio (10 min)

`git clone` descarga una copia completa de un repositorio remoto a tu computadora — es lo que vas a usar para trabajar en el proyecto en equipo más adelante.

```bash
cd ..
git clone https://github.com/TU-USUARIO/lab1-git.git lab1-git-clon
cd lab1-git-clon
ls
```

Deberías ver el mismo `notas.txt` dentro de la nueva carpeta.

---

## Parte 8 — Repaso de comandos (para tu referencia)

| Comando | Qué hace |
|---|---|
| `git init` | Convierte la carpeta actual en un repositorio Git |
| `git status` | Muestra el estado actual (qué cambió, qué está listo para commit) |
| `git add <archivo>` | Marca un archivo para incluirlo en el próximo commit |
| `git commit -m "mensaje"` | Guarda los cambios marcados, con un mensaje |
| `git log` | Muestra el historial de commits |
| `git remote add origin <url>` | Conecta el repo local con uno remoto en GitHub |
| `git push` | Sube tus commits al repositorio remoto |
| `git clone <url>` | Descarga una copia de un repositorio remoto |
| `git pull` | Trae los cambios más recientes del repositorio remoto |

---

## Entregable del laboratorio

Envía al profesor (por el medio indicado en clase) el enlace de tu repositorio `lab1-git` en GitHub, con al menos **2 commits** visibles en el historial.

---

## Próximo laboratorio (Lab 2)

En el Lab 2 vamos a usar **Visual Studio Code** (ya instalado en las computadoras del laboratorio) para escribir y ejecutar programas en C++, y vamos a repetir este mismo flujo de Git/GitHub pero **desde dentro del IDE**, usando el panel de Control de Versiones en vez de la consola.
