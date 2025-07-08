# Vim Editor Basic Commands & Controls

Vim is a powerful text editor available in almost all Linux systems. Below are essential Vim commands and controls for beginners and intermediate users.

---

## 🔹 Modes in Vim

| Mode | How to Enter | Purpose |
|-----|--------------|---------|
| Normal Mode | Press `Esc` | Default mode for navigation and commands |
| Insert Mode | Press `i`, `I`, `a`, `A`, `o`, `O` | For editing and inserting text |
| Visual Mode | Press `v`, `V`, or `Ctrl + v` | For selecting text |
| Command-Line Mode | Press `:` in Normal mode | To enter commands (e.g., save, quit) |

---

## 🔹 Basic Vim Controls

| Command | Description |
|--------|-------------|
| `i` | Insert before cursor |
| `I` | Insert at the beginning of the line |
| `a` | Append after cursor |
| `A` | Append at the end of the line |
| `o` | Open a new line **below** |
| `O` | Open a new line **above** |
| `!<any commands>` | you can use any commands inside the vim |
| `Esc` | Return to Normal Mode from Insert/Visual modes |

---

## 🔹 Saving and Exiting

| Command | Description |
|--------|-------------|
| `:w` | Save file (write changes) |
| `:q` | Quit Vim |
| `:wq` | Save and quit |
| `:q!` | Quit **without saving** |
| `ZZ` | Save and quit (**same as `:wq`**) |

---

## 🔹 Navigation

| Command | Description |
|--------|-------------|
| `h` | Move cursor **left** |
| `l` | Move cursor **right** |
| `j` | Move cursor **down** |
| `k` | Move cursor **up** |
| `0` | Move to the **start of the line** |
| `$` | Move to the **end of the line** |
| `gg` | Go to the **top of the file** |
| `G` | Go to the **bottom of the file** |
| `:` + line number | Go to specific line |

---

## 🔹 Editing Commands

| Command | Description |
|--------|-------------|
| `x` | Delete character under cursor |
| `dd` | Delete **entire line** |
| `dw` | Delete word |
| `yy` | Copy (yank) line |
| `p` | Paste after cursor |
| `u` | Undo last action |
| `Ctrl + r` | Redo last undone change |

---

## 🔹 Search in Vim

| Command | Description |
|--------|-------------|
| `/word` | Search for "word" in the file |
| `n` | Go to the **next occurrence** |
| `N` | Go to the **previous occurrence** |

---

## ✅ Basic Usage Example

1. Open a file:
   ```bash
   vim filename.txt

