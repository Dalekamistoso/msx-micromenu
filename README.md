<img width="960" height="720" alt="MENU-MSX2" src="https://github.com/user-attachments/assets/2c92110b-41ea-422e-9842-3e8e9ab5d8de" />
<img width="1280" height="960" alt="MENU-MSX1" src="https://github.com/user-attachments/assets/55f30039-cb43-4294-bf4d-690b207375a5" />
# MicroMenu by DrWh0 / Dalekamistoso

Configurable program launcher for  **MSX-DOS 2**

---

## Characteristics

- **Customizable setup editing a single text file** (`MENU.INI`): Easily add/remove/rename programs
- **Customizable Menu title**: Automatically selfcenters text in the header of the menu
- **Nice graphic alike text menu box** centered according longest text in item list
- **Automatic MSX1 / MSX2 or better video detection**:
  - MSX2 or better: 80 width screen and selected option with a nice **real inverted background** (vía VRAM capabilities)
  - MSX1: 40 width screen using a simple text `>` symbol compatible with all MSX1 character text set
- **Automatic detection of MSX-DOS 2**: If system is not compatible will refuse to run
- **Easy navigation**:
  - `↑` / `↓`: Moves up/down in the list of programs.
  - `←` / `→`: Moves quickly between multiple pages of options
  - `ENTER`: Executes the current highlighted program
  - `ESC`: Exits from program and returns to MSX-DOS2.
- **No annoying "keyclicks"** While you are in the launcher, it will reactivate when exiting.
- **Highly compact**: Barely more than 3KB of disk space only two files, executable (~3,5kb & menu.ini
- **No graphic garbage or memory leaks behind**: VRAM & RAM properly cleaned, no hit on perfomance or loss of free memory 
- **No complicated dependencies 100% made in assembler** Compiled only with SjASMPlus 

---

## `MENU.INI` File usage and details

The file must be **in the same folder** that main executable (MENU.COM)

Format of the file:

```ini
[TITULO]      <-----FIELD THAT DEFINES THE TEXT HEADER
text=MSXMENU  <-----TEXT HEADER OF THE MENU PROGRAM

[PROGRAMS]    <-----FIELD THAT DEFINES THE START OF THE LIST OF PROGRAMS (IN ORDER FROM UP TO DOWN)
text=Ejecutar Device Info  <-----DESCRIPTION OF THE PROGRAM 
exec=\devinfo.com          <-----FILE TO EXECUTE AND PATH (SUPPORTS RELATIVE AND FIXED PATHS)

text=Ejecutar BASIC        <-----DESCRIPTION OF THE SECOND PROGRAM TO SHOW
exec=BASIC                 <-----FILE TO EXECUTE AND PATH OF THE PROGRAM DESCRIBED IN THE PREVIOUS LINE

text=Ejecutar un juego     <----- THE THIRD ONE AND SO ....
exec=a:\juegos\milagro.com
```

### Sections (I explain again in a more detailed way)

| Section      | Mandatory | Description                                                       |
|--------------|-----------|-------------------------------------------------------------------|
| `[TITULO]`   | No        | FIELD THAT DEFINES THE TEXT HEADER OF THE MENU CENTERED AT THE TOP|
| `[PROGRAMS]` | Yes       | SECTION WITH THE LIST OF PROGRAMS AS MENTIONED EARLIER            |

Remember that each programs is defined with **TWO consecutive lines**:

```ini
text=<name showed in menu>
exec=<path and file to execute>
```

- The blank lines and the order of the `text=`/`exec=` pairs are free; just keep adding two-line blocks for each program.
- `text=` supports upto **80 characters**.
- `exec=` supports upto **128 characters** as path limitation
- Upto **20 programas** in the menu (but you can launch another menu instance in other folder with other list)

### Important limitation in `exec=`

In order to launch a program, `MSXMENU` writes in the command line **directly in the BIOS of keyboard buffer**, 
which is basically only 40 bytes. 

For security, the path that is "typed" is limited to the first **30 characters**. 
If your path is longer, the option will look and be selected correctly in the menu, but when executed, it will launch a truncated (incorrect) command. 
Keep `exec=` paths reasonably short.

---

## Quick usage manual

1. Copy `MENU.COM` & your customized `MENU.INI` (and obviously the programs you want to launch) 
2. From MSX-DOS2/Nextor command prompt type:
   ```
   MENU
   ```
3. You will see the text menu box with the title you provided (if set) and list of programs you provided.
4. Use keyboard cursors `↑`/`↓`, or jump to next or previous page with `←`/`→` if there are more programs that can be listed in the same screen.
5. Press `ENTER` key over the selected option you want to launch or `ESC` key to exit to MSX-DOS prompt.

---

## Extra technical notes (you can ignore this if you are not a developer)

- This program requieres **MSX-DOS 2** (paths and many file functions uses "handle" not present in MSX-DOS 1). 
- If **MSX-DOS 1** is detected an error will be shown and execution will be cancelled.
- 80 columns text mode (MSX2 or better) and color highlight uses BIOS calls using **inter-slot calls** (`CALSLT`) needed under MSX-DOS2.
- Highlight on MSX2+ is implemented writing in blitter table of color/blinking in VRAM of 80 columns text mode (T2).
- Compiled with [sjasmplus](https://github.com/z00m128/sjasmplus).

---

## Estructura del proyecto

```
menu.asm              Punto de entrada; incluye el resto de fuentes
src/main.asm           Programa principal: pantalla, menu, navegacion, lanzamiento
src/ini_parser.asm     Lectura y parseo de MENU.INI
include/system.inc     Constantes de sistema (teclas, VRAM, colores...)
include/bios.inc       Direcciones de rutinas de la BIOS
include/dos.inc        Numeros de funcion de MSX-DOS
data/MENU.INI          Ejemplo de configuracion
build.bat              Script de compilacion
```
