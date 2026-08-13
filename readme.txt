# MicroMenu by DrWh0 / Dalekamistoso

Configurable launcher for MSX-DOS 2

---

## Characteristics

- Easy setup editing `MENU.INI` file
- Easy to add/remove/rename programs
- Customizable Menu title
- Automatically centers text in header
- Nice graphic alike text menu box
- Automatic MSX1/MSX2/2+ detection:
  - MSX2 or better: 80 width screen
    Selected option with a nice bar
  - MSX1: 40 width screen 
    Selected option with `>` symbol
- Automatic detection of MSX-DOS 2
- Easy navigation:
- Cursors: Moves up/down in the list
  Cursors: Moves between pages (L/R)
- `ENTER`: Executes selected program
- `ESC`: Exits from program
- No annoying keyclicks in the launcher
- Compact: Barely ~3KB only 2 files
- Properly cleans RAM/VRAM no garbage
- No memory impact in programs
- No weird dependencies 100% ASM
- Compiled only with SjASMPlus
- Relative & fixed paths accepted


---

## `MENU.INI` File usage and details

Both files must be in the same folder

Format of the file:

```ini
[TITLE]      <-DEFINES THE TEXT HEADER
text=MSXMENU <-TEXT HEADER OF THE MENU

[PROGRAMS]   <-PROGRAM LIST (UP->DOWN)
text=Program's description
exec=\program.com (drive:\path format)

text=Run BASIC (Another example)
exec=BASIC (Direct command to run) 

```

### Sections

| Section    | Mandatory | Description|
|------------|-----------|------------|
|`[TITLE]`   | No        | MENU TITLE |
|`[PROGRAMS]`| Yes       | PROGR. LIST|

Remember that each program is defined 
with **TWO consecutivee lines**:

```ini
text=<name showed in menu>
exec=<path and file to execute>
```

- The blank lines and the order of the 
  `text=`/`exec=` pairs are free; just
  keep adding two-line blocks for each
  program.
- `text=` supports upto 80 characters
- `exec=` supports upto 128 characters
          (path limitation)
- Upto 20 programas in the menu 

**  But you can launch another menu
    instance in other folder with
    additional list of programs

### Important limitation in `exec=`

In order to launch a program `MSXMENU`
writes in the command line directly 
in the BIOS of keyboard buffer, which
is basically only 40 bytes.

For security, the path that is "typed"
is limited to the first 30 characters.

If path is longer, the option will
look & be selected correctly but
will launch a truncated/incorrect 
command.

Keep `exec=` paths reasonably short.

---

## Quick usage manual

1. Copy `MENU.COM`+`MENU.INI` together
2. Edit and customize your `MENU.INI
3. From MSX-DOS2/Nextor prompt type:
  ```
  MENU
  ```
4. You will see the text menu box with
   the title you provided (if set) & 
   list of programs you provided.
5. Use keyboard cursors up/down or
   right/left to jump to next or
   previous page  if more programs 
   can be listed in the same screen.
6. Press `ENTER` key over the selected 
   option you want to launch or `ESC` 
   key to exit to MSX-DOS prompt.

---

## Credits:

Program made by:
Carlos Romero (DrWh0/Dalekamistoso)
Version 1.1 (2026/08/12)

Check my github for more projects: 
https://www.github.com/Dalekamistoso
so
