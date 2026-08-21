# Tutorial Básico de Terminal
## COEN 2210 — Introduction to Programming

Este tutorial cubre lo mínimo necesario para moverte cómodamente en la terminal antes de empezar el Lab 1. No necesitas memorizar nada — puedes volver a este archivo cuando lo necesites.

Vamos a aprender los comandos siguiendo un ejemplo completo: crear una carpeta de práctica, movernos dentro de ella, crear y editar un archivo de texto, y luego limpiar todo al final. Cada comando incluye qué hace, cómo se usa, y qué deberías ver después de ejecutarlo.

**¿Windows o Mac/Linux?** Los comandos varían un poco según el sistema — cada paso muestra ambas versiones. Usa la que corresponda a tu computadora.

**Cómo abrir la terminal:**
- **Windows:** busca "PowerShell" o "cmd" en el menú de inicio.
- **Mac:** `Cmd + Espacio` (Spotlight), escribe "Terminal", presiona Enter.
- **Linux:** depende de tu distribución, usualmente `Ctrl + Alt + T`.

---

## Paso 1 — ¿Dónde estoy parado?

Cuando abres la terminal, siempre estás "parado" dentro de alguna carpeta — igual que cuando abres el Explorador/Finder y ves el contenido de una carpeta específica. Antes de crear nada, vamos a confirmar dónde estamos.

> 💻 **Vas a usar la terminal.** Escribe el siguiente comando y presiona `Enter`:

**Windows (PowerShell/cmd):**
```powershell
cd
```

**Mac/Linux:**
```bash
pwd
```

**¿Qué hace esto?** Muestra la ruta completa de la carpeta donde estás parado ahora mismo.

**Qué deberías ver:** algo como `C:\Users\tunombre` (Windows) o `/Users/tunombre` (Mac) o `/home/tunombre` (Linux). Si no reconoces esa ubicación, no te preocupes — normalmente es tu carpeta de usuario por defecto.

Ahora veamos qué hay dentro de esa carpeta:

**Windows:**
```powershell
dir
```

**Mac/Linux:**
```bash
ls
```

**Qué deberías ver:** una lista de carpetas y archivos, probablemente cosas como `Documents`, `Desktop`, `Downloads`.

---

## Paso 2 — Crear nuestra carpeta de práctica

Vamos a crear una carpeta llamada `practica-terminal` para hacer todos los ejercicios de este tutorial sin desordenar tus otros archivos.

> 💻 **Vas a usar la terminal.** Escribe (ambos sistemas usan el mismo comando):

```bash
mkdir practica-terminal
```

**¿Qué hace esto?** Crea una carpeta nueva llamada `practica-terminal`, dentro de la carpeta donde estás parado.

**Qué deberías ver:** ningún mensaje (si `mkdir` no muestra nada, significa que funcionó). Para confirmar que sí se creó, vuelve a listar el contenido:

**Windows:**
```powershell
dir
```

**Mac/Linux:**
```bash
ls
```

**Qué deberías ver:** `practica-terminal` ahora aparece en la lista, junto a lo que ya había antes.

---

## Paso 3 — Entrar a la carpeta

> 💻 **Vas a usar la terminal.** Escribe (ambos sistemas usan el mismo comando):

```bash
cd practica-terminal
```

**¿Qué hace esto?** Te mueve *dentro* de la carpeta `practica-terminal` — de ahora en adelante, todo lo que crees ocurre ahí, no en la carpeta de donde venías.

**Confirma dónde estás ahora:**

**Windows:**
```powershell
cd
```

**Mac/Linux:**
```bash
pwd
```

**Qué deberías ver:** la misma ruta de antes, pero ahora con `\practica-terminal` (Windows) o `/practica-terminal` (Mac/Linux) al final — confirma que sí entraste.

> **Para subir un nivel y salir de la carpeta** (lo vamos a usar más adelante), el comando es el mismo en ambos sistemas: `cd ..`

---

## Paso 4 — Crear un archivo con contenido (`echo` y `>`)

Ahora vamos a crear un archivo de texto llamado `notas.txt` con una línea de contenido adentro, usando `echo` (que normalmente solo muestra texto en pantalla) combinado con `>` (que redirige ese texto hacia un archivo en vez de mostrarlo).

> 💻 **Vas a usar la terminal.** Escribe (ambos sistemas usan el mismo comando):

```bash
echo "Mi primera linea de texto" > notas.txt
```

**¿Qué hace esto?** Crea el archivo `notas.txt` (si no existía) y escribe adentro el texto `Mi primera linea de texto`.

**Qué deberías ver:** ningún mensaje en pantalla. Para confirmar que el archivo se creó, lístalo:

**Windows:**
```powershell
dir
```

**Mac/Linux:**
```bash
ls
```

**Qué deberías ver:** `notas.txt` aparece en la lista.

**Ahora veamos qué hay adentro del archivo, sin abrirlo en un editor:**

**Windows:**
```powershell
type notas.txt
```

**Mac/Linux:**
```bash
cat notas.txt
```

**Qué deberías ver:** `Mi primera linea de texto` impreso en la terminal — es el contenido del archivo.

### La diferencia entre `>` y `>>`

Vamos a agregar una segunda línea, pero esta vez sin borrar la primera. Para eso se usa `>>` (dos veces el símbolo) en vez de `>`:

```bash
echo "Mi segunda linea de texto" >> notas.txt
```

**¿Qué hace esto distinto al paso anterior?** `>>` agrega el texto **al final** del archivo existente, sin borrar lo que ya había. Si hubieras usado `>` otra vez, la primera línea se habría borrado y reemplazado por completo.

**Confirma el resultado:**

**Windows:**
```powershell
type notas.txt
```

**Mac/Linux:**
```bash
cat notas.txt
```

**Qué deberías ver:** ahora **dos** líneas — "Mi primera linea de texto" y "Mi segunda linea de texto", en ese orden.

---

## Paso 5 — Crear una subcarpeta

Vamos a organizar un poco más creando una carpeta adentro de `practica-terminal`.

> 💻 **Vas a usar la terminal.** Escribe (ambos sistemas usan el mismo comando):

```bash
mkdir subcarpeta
cd subcarpeta
```

**¿Qué hace cada comando?**
- `mkdir subcarpeta` — crea la carpeta nueva.
- `cd subcarpeta` — te mueve adentro de ella.

**Confirma dónde estás:**

**Windows:** `cd`
**Mac/Linux:** `pwd`

**Qué deberías ver:** la ruta ahora termina en `\practica-terminal\subcarpeta` (Windows) o `/practica-terminal/subcarpeta` (Mac/Linux).

Regresa a la carpeta anterior antes de continuar:

```bash
cd ..
```

**Qué deberías ver (al confirmar con `cd` o `pwd`):** la ruta vuelve a terminar en `practica-terminal`, sin `subcarpeta` al final.

---

## Paso 6 — Limpieza: eliminar el archivo y las carpetas

> ⚠️ **Cuidado antes de empezar esta parte:** a diferencia de borrar algo desde el Explorador/Finder, **eliminar desde la terminal no manda nada a la Papelera/Basura** — se borra directamente y no hay forma fácil de recuperarlo. Verifica bien el nombre antes de presionar Enter.

**Eliminar el archivo `notas.txt`:**

**Windows:**
```powershell
del notas.txt
```

**Mac/Linux:**
```bash
rm notas.txt
```

**Qué deberías ver:** ningún mensaje. Confirma con `dir`/`ls` — `notas.txt` ya no debería aparecer.

**Eliminar la subcarpeta vacía:**

**Windows:**
```powershell
rmdir subcarpeta
```

**Mac/Linux:**
```bash
rmdir subcarpeta
```

**Qué deberías ver:** ningún mensaje, y `subcarpeta` desaparece de la lista al confirmar con `dir`/`ls`.

> **Nota:** `rmdir` solo funciona en carpetas **vacías**. Si la carpeta todavía tiene archivos adentro, necesitas `rmdir /s nombre-carpeta` (Windows) o `rm -r nombre-carpeta` (Mac/Linux) — el modificador le dice "elimina la carpeta y todo lo que tenga adentro, sin preguntar una por una".

**Salir y eliminar `practica-terminal` por completo (ya vacía):**

```bash
cd ..
```

**Windows:**
```powershell
rmdir practica-terminal
```

**Mac/Linux:**
```bash
rmdir practica-terminal
```

**Qué deberías ver:** al confirmar con `dir`/`ls`, `practica-terminal` ya no aparece — quedaste exactamente como al principio del tutorial.

---

## Paso 7 — Terminal ↔ Explorador/Finder

Esto es útil para cuando quieras confirmar visualmente dónde estás, o para saltar directo a la terminal desde una carpeta que ya abriste con el mouse.

### De la terminal al Explorador/Finder

Estando parado en cualquier carpeta (usa `cd`/`pwd` para confirmar dónde estás):

**Windows:**
```powershell
explorer .
```

**Mac:**
```bash
open .
```

**Linux:**
```bash
xdg-open .
```

**¿Qué hace esto?** El `.` significa "la carpeta actual" — abre una ventana del Explorador/Finder mostrando exactamente donde estás parado en la terminal.

**Qué deberías ver:** una ventana nueva del Explorador de Archivos (Windows) o Finder (Mac) mostrando esa misma carpeta.

### Del Explorador/Finder a la terminal

Esto es útil cuando ya navegaste visualmente hasta una carpeta y quieres abrir la terminal ahí directamente, sin escribir varios `cd`.

- **Windows:** dentro de la carpeta en el Explorador de Archivos, haz clic en la barra de direcciones (arriba), escribe `cmd` o `powershell`, y presiona Enter. *(Alternativa: clic derecho dentro de la carpeta → "Abrir en Terminal", si tu versión de Windows lo incluye.)*
- **Mac:** clic derecho sobre la carpeta en el Finder → si no ves "Nueva Terminal en la carpeta", actívalo una vez en **Finder → Configuración (Preferencias) → Barra de herramientas → agregar "Nueva Terminal en carpeta"**.

**Qué deberías ver:** una terminal nueva que abre ya parada directamente en esa carpeta (confírmalo con `cd`/`pwd`), sin necesidad de navegar con comandos.

---

## Resumen rápido (Windows vs Mac/Linux)

| Acción | Windows | Mac/Linux |
|---|---|---|
| Dónde estoy | `cd` | `pwd` |
| Listar contenido | `dir` | `ls` |
| Entrar a carpeta | `cd nombre` | `cd nombre` |
| Subir un nivel | `cd ..` | `cd ..` |
| Crear carpeta | `mkdir nombre` | `mkdir nombre` |
| Eliminar carpeta vacía | `rmdir nombre` | `rmdir nombre` |
| Eliminar carpeta con contenido | `rmdir /s nombre` | `rm -r nombre` |
| Eliminar archivo | `del archivo.txt` | `rm archivo.txt` |
| Escribir texto a un archivo (nuevo, borra lo anterior) | `echo "texto" > archivo.txt` | `echo "texto" > archivo.txt` |
| Agregar texto a un archivo (sin borrar) | `echo "texto" >> archivo.txt` | `echo "texto" >> archivo.txt` |
| Ver contenido de un archivo | `type archivo.txt` | `cat archivo.txt` |
| Abrir carpeta actual en Explorador/Finder | `explorer .` | `open .` |

---

Con esto ya tienes lo necesario para empezar el **Lab 1 — Git y GitHub desde la Consola**.
