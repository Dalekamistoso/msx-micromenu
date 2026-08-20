---
## MicroMenu by DrWh0 / Dalekamistoso

Configurable program launcher for  **MSX-DOS 2**

---
<img width="960" height="720" alt="MENU-MSX0" src="https://github.com/user-attachments/assets/c280c7cc-05a0-48cb-a09f-38fb9d0a9803" /><img width="960" height="720" alt="MENU-MSX4" src="https://github.com/user-attachments/assets/1ef13c87-d255-4037-8a19-cd0f05e73591" />
<img width="960" height="720" alt="MENU-MSX3" src="https://github.com/user-attachments/assets/390766f3-124f-4275-98ae-9b427aad55f6" />
<img width="960" height="720" alt="MENU-MSX2" src="https://github.com/user-attachments/assets/11cce8bf-25be-4e2c-98d9-9a83b2292670" />
<img width="1280" height="960" alt="MENU-MSX1" src="https://github.com/user-attachments/assets/fa50f80e-ff0c-463e-beb7-3b5b041ad266" />


---

## Characteristics

- **Customizable setup editing a single text file** (`MENU.INI`): Easily add/remove/rename programs
- **Customizable Menu title**: Automatically selfcenters text in the header of the menu
- **Customizable color schema**: Choose your favorite colours
- **Nice graphic alike text menu box** centered according longest text in item list
- **Automatic MSX1 / MSX2 or better video detection**:
  - MSX2 or better: 80 width screen & selected option with a nice **real inverted background** (vía VRAM)
  - MSX1: 40 width screen using a simple text `>` symbol compatible with all MSX1 character text set
- **Automatic detection of MSX-DOS 2**: If system is not compatible will refuse to run
- **Easy navigation**:
  - `↑` / `↓`: Moves up/down in the list of programs.
  - `←` / `→`: Moves quickly between multiple pages of options
  - `ENTER`: Executes the current highlighted program
  - `ESC`: Exits from program and returns to MSX-DOS2.
- **Launches programs from their own folder**: if `exec=` includes a path, MicroMenu changes into that directory (via MSX-DOS2) before running the program, so programs that expect their own data files in the current directory work correctly.
- **Optional custom screen colors** via a `[COLOR]` section in `MENU.INI` (MSX `COLOR ink,paper,border` format), original colors are restored automatically before the selected program runs, and on exit.
- **No annoying "keyclicks"** While you are in the launcher, it will reactivate when exiting.
- **Highly compact**: Barely more than 3KB of disk space only two files, executable (~3,5kb & menu.ini
- **No graphic garbage or memory leaks behind**: VRAM+RAM fully cleaned, no hit on perfomance/free memory 
- **No complicated dependencies 100% made in assembler** Compiled only with SjASMPlus 

---

## `MENU.INI` File usage and details

The file must be **in the same folder** that main executable (MENU.COM)

Format of the file:

```ini
[TITLE]       <-----OPTIONAL FIELD, DEFINES THE TEXT HEADER ([TITULO] in 1.0)
text=MSXMENU  <-----TEXT HEADER OF THE MENU PROGRAM

[COLOR]                <-----OPTIONAL FIELD, CUSTOM SCREEN COLORS
color=15,1,1           <-----Ink,Paper,Border (MSX COLOR STANDARD VALUES 0-15)

[PROGRAMS]    <-----FIELD THAT DEFINES THE START OF THE LIST OF PROGRAMS (IN ORDER FROM UP TO DOWN)
text=Run Device Info   <-----DESCRIPTION OF THE PROGRAM 
exec=\devinfo.com      <-----FILE TO EXECUTE AND PATH (SUPPORTS RELATIVE AND FIXED PATHS)

text=Run BASIC         <-----DESCRIPTION OF THE SECOND PROGRAM TO SHOW
exec=BASIC             <-----FILE TO EXECUTE AND PATH OF THE PROGRAM DESCRIBED IN THE PREVIOUS LINE

text=Run a game        <----- THE THIRD ONE AND SO ....
exec=a:\games\miracle.com
```

### Sections (I explain again in a more detailed way)

| Section      | Mandatory | Description                                                       |
|--------------|-----------|-------------------------------------------------------------------|
| `[TITLE]`    | No        | DEFINED TEXT HEADER OF THE MENU CENTERED AT THE TOP               |
| `[COLOR]`    | No        | DEFINED TEXT COLOURS USING "COLOR" MSX COMMAND SYNTAX             |
| `[PROGRAMS]` | Yes       | SECTION WITH THE LIST OF PROGRAMS AS MENTIONED EARLIER            |

If [TITLE] is not present menu will show without header block, only footer block
If [COLOR] is not present menu will be shown with current system colours
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
4. Use keyboard cursors `↑`/`↓`, or jump to next/previous page with `←`/`→` if list is too long to fit on screen.
5. Press `ENTER` key over the selected option you want to launch or `ESC` key to exit to MSX-DOS prompt.

---

## Credits:
Program made by Carlos Romero (DrWh0 / Dalekamistoso) 2026/08/13

Check my github for more projects:
www.github.com/Dalekamistoso

