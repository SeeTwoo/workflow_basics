# 🛠️ Workflow Basics: Neovim & GDB

A quick reference guide for editing with **(Neo)vim** and debugging with **GDB**.

---

## Table of Contents
- [Vim & Neovim](#-vim--neovim)
  - [The Concept of Modes](#the-concept-of-modes)
  - [Normal Mode: Moving Around](#1-moving-around-motions)
  - [Normal Mode: Editing Actions](#2-editing-actions-operators)
  - [The Magic: Verb + Motion](#3-the-magic-combining-actions--motions)
  - [Entering Insert Mode](#entering-insert-mode)
  - [Command Mode](#command-mode-)
  - [Configuration](#configuration)
- [GDB (GNU Debugger)](#-gdb-gnu-debugger)
  - [Compiling for Debugging](#1-compiling-for-debugging)
  - [Launching GDB](#2-launching-gdb)
  - [Essential GDB Commands](#3-essential-commands)
  - [Understanding `step` vs `next`](#step-vs-next-example)

---

## 🟢 Vim & Neovim

Vim is built around **modes**. The three most important are:
1. **Normal mode** (Default): Where you navigate, delete, copy, and manipulate text.
2. **Insert mode**: Where typing keys actually writes text to the buffer (like a regular text editor).
3. **Command mode**: Where you issue instructions to the editor (saving, quitting, searching).

> [!TIP]
> Treat Insert mode like a **surgical strike**: jump in, type the text you need, and press <kbd>Esc</kbd> immediately to go back to Normal mode.

---

### 1. Moving Around (Motions)

Return to Normal mode at any time with <kbd>Esc</kbd>.

| Key | Description |
| :--- | :--- |
| <kbd>h</kbd> <kbd>j</kbd> <kbd>k</kbd> <kbd>l</kbd> | Move **left**, **down**, **up**, and **right** |
| <kbd>w</kbd> | Jump to the **start** of the next word |
| <kbd>e</kbd> | Jump to the **end** of the next word |
| <kbd>b</kbd> | Jump **backward** to the previous word |
| <kbd>_</kbd> or <kbd>^</kbd> | Jump to the first non-whitespace character on the line |
| <kbd>g</kbd><kbd>g</kbd> | Jump to the **very top** of the file |
| <kbd>G</kbd> | Jump to the **very bottom** of the file |
| `<N>`<kbd>g</kbd><kbd>g</kbd> | Jump to line `<N>` *(e.g., `21gg` jumps to line 21)* |

---

### 2. Editing Actions (Operators)

| Key | Action | Double-tap for whole line |
| :--- | :--- | :--- |
| <kbd>d</kbd> | **Delete** (cuts text) | <kbd>d</kbd><kbd>d</kbd> → Deletes current line |
| <kbd>y</kbd> | **Yank** (copies text) | <kbd>y</kbd><kbd>y</kbd> → Copies current line |
| <kbd>p</kbd> | **Paste** after cursor | — |
| <kbd>c</kbd> | **Change** (deletes & enters Insert mode) | <kbd>c</kbd><kbd>c</kbd> → Changes current line |

---

### 3. The Magic: Combining Actions + Motions

Vim behaves like a language: **`Verb + Motion`**.

* `dw` → **D**elete to the next **w**ord
* `d3gg` → **D**elete everything from current line to line **3**
* `dG` → **D**elete everything from cursor to the **end of file**
* `da{` → **D**elete **A**round `{ ... }` *(deletes the entire enclosing block)*

> [!NOTE]
> **Do not panic!** You do not need to memorize all of these at once. If you find yourself repeatedly pressing an annoying key sequence, there is almost certainly a 2-key Vim shortcut for it.

---

### Entering Insert Mode

| Key | How it enters Insert mode |
| :--- | :--- |
| <kbd>i</kbd> | **I**nsert *before* the cursor |
| <kbd>a</kbd> | **A**ppend *after* the cursor |
| <kbd>A</kbd> | Append at the **end of the line** |
| <kbd>o</kbd> | Open a new line **below** and insert |
| <kbd>O</kbd> | Open a new line **above** and insert |

---

### Command Mode (`:`)

Press <kbd>:</kbd> from Normal mode to enter Command mode:

| Command | Action |
| :--- | :--- |
| `:w` | Write (save) file |
| `:w <name>` | Save as `<name>` |
| `:q` | Quit |
| `:wq` or `:x` | Write and quit |
| `:q!` | Force quit without saving |
| `:e <filename>` | Edit another file in the same window |

---

### Configuration

* **Vim** config file: `~/.vimrc` *(uses Vimscript)*
* **Neovim** config file: `~/.config/nvim/init.lua` *(uses Lua)*

#### Example: Enabling Line Numbers

**In Vim (`~/.vimrc`):**
```vim
set number
