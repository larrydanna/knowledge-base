# VSCode Keyboard Shortcuts — Workflow Reference

**Date:** 2026-04-13  
**Category:** environment  
**Tags:** `vscode`, `keyboard`, `shortcuts`, `productivity`, `workflow`  
**Related:** [VSCode: Set Markdown Preview as Default](vscode-markdown-preview-default-260413a.md) · [Workstation Setup — Windows 10 / 11](workstation-setup-windows-260413a.md)

> **Living document.** Focused on UI and workflow control — the things that reduce reaching for the mouse.  
> All shortcuts listed for **Windows**. On **macOS**, substitute `Ctrl` → `⌘ Cmd` and `Alt` → `⌥ Option` unless noted otherwise.  
> On **Linux**, shortcuts match Windows.

---

## TL;DR — Most Valuable Shortcuts

| Shortcut | What it does |
|----------|-------------|
| `Ctrl+Shift+P` | Command Palette — the most important shortcut |
| `Ctrl+P` | Quick Open a file by name |
| `Ctrl+J` | Toggle the bottom Panel (Terminal, Output, etc.) |
| `Ctrl+B` | Toggle the Primary Sidebar |
| `Ctrl+\`` | Toggle integrated terminal |
| `Ctrl+\` | Split editor |
| `Ctrl+D` | Select next occurrence of word |
| `Alt+Up/Down` | Move line up/down |
| `Shift+Alt+Down` | Duplicate line |
| `Ctrl+Shift+K` | Delete line |
| `F12` | Go to Definition |
| `Ctrl+.` | Quick Fix / light bulb actions |
| `F2` | Rename symbol |
| `Shift+Alt+F` | Format document |
| `Ctrl+K Z` | Toggle Zen Mode |

---

## Command Palette & Quick Access

The Command Palette is the gateway to everything. If you forget a shortcut, open it and type what you want.

| Shortcut | Action |
|----------|--------|
| `Ctrl+Shift+P` | Open Command Palette |
| `Ctrl+P` | Quick Open — go to any file by name |
| `Ctrl+P` then `>` | Switch to Command Palette from Quick Open |
| `Ctrl+P` then `@` | Go to Symbol in current file |
| `Ctrl+P` then `#` | Go to Symbol in workspace |
| `Ctrl+P` then `:` | Go to line number |
| `Ctrl+T` | Go to Symbol in workspace (direct) |
| `Ctrl+G` | Go to Line / Column |
| `Ctrl+Shift+O` | Go to Symbol in current file (direct) |

> **Tip:** `Ctrl+P` with a filename supports fuzzy matching — `ucm` will find `UserControllerManager.cs`.

---

## Panels, Sidebar & View Toggles

### Primary Sidebar

| Shortcut | Action |
|----------|--------|
| `Ctrl+B` | Toggle Primary Sidebar open/closed |
| `Ctrl+Shift+E` | Show Explorer (files) |
| `Ctrl+Shift+F` | Show Search |
| `Ctrl+Shift+G` | Show Source Control |
| `Ctrl+Shift+D` | Show Run & Debug |
| `Ctrl+Shift+X` | Show Extensions |

### Secondary Sidebar & Activity Bar

| Shortcut | Action |
|----------|--------|
| `Ctrl+Alt+B` | Toggle Secondary Sidebar (right side) |
| `Ctrl+Shift+P` → "Focus Activity Bar" | Move focus to the icon bar on the left |

### Bottom Panel (Terminal area)

| Shortcut | Action |
|----------|--------|
| `Ctrl+J` | Toggle bottom Panel open/closed |
| `Ctrl+\`` | Toggle integrated Terminal specifically |
| `Ctrl+Shift+\`` | Open a new Terminal |
| `Ctrl+Shift+Y` | Show Debug Console |
| `Ctrl+Shift+U` | Show Output panel |
| `Ctrl+Shift+M` | Show Problems panel |

> **Tip:** `Ctrl+J` collapses the entire panel area at once — faster than closing terminal/output individually.

### Full Screen & Focus Modes

| Shortcut | Action |
|----------|--------|
| `F11` | Toggle Full Screen |
| `Ctrl+K Z` | Toggle Zen Mode (hides everything except the editor) |
| `Ctrl+K Ctrl+W`... | (see Editor Tabs section) |
| `Ctrl+=` / `Ctrl+-` | Zoom in / Zoom out (entire UI) |
| `Ctrl+Shift+.` | Focus Breadcrumbs (path bar above editor) |

---

## Editor Tabs & Groups (Split Panes)

### Opening & Closing Tabs

| Shortcut | Action |
|----------|--------|
| `Ctrl+W` | Close current tab |
| `Ctrl+K Ctrl+W` | Close all tabs |
| `Ctrl+Shift+T` | Reopen last closed tab |
| `Ctrl+Tab` | Cycle forward through open tabs |
| `Ctrl+Shift+Tab` | Cycle backward through open tabs |
| `Ctrl+PageDown` | Next tab |
| `Ctrl+PageUp` | Previous tab |
| `Ctrl+K Ctrl+Enter` | Pin / unpin active tab |

### Split Editor & Groups

| Shortcut | Action |
|----------|--------|
| `Ctrl+\` | Split editor (new group to the right) |
| `Ctrl+K Ctrl+\` | Split editor down (new group below) |
| `Ctrl+1` | Focus editor group 1 |
| `Ctrl+2` | Focus editor group 2 |
| `Ctrl+3` | Focus editor group 3 |
| `Ctrl+K Left/Right` | Move active editor to the group on left/right |
| `Ctrl+K Ctrl+Left/Right` | Focus into group on left/right |
| `Ctrl+Alt+Left/Right` | Move tab to previous/next group |

### Navigation History

| Shortcut | Action |
|----------|--------|
| `Alt+Left` | Navigate back (like browser back button) |
| `Alt+Right` | Navigate forward |

> **Tip:** `Alt+Left` is invaluable after `F12` (Go to Definition) — it jumps you back to where you came from.

---

## Terminal

| Shortcut | Action |
|----------|--------|
| `Ctrl+\`` | Toggle terminal panel |
| `Ctrl+Shift+\`` | Create new terminal |
| `Ctrl+Shift+5` | Split current terminal (side by side) |
| `Alt+Left/Right` | Navigate between split terminal panes |
| `Ctrl+PageUp/Down` | Scroll terminal output one page |
| `Ctrl+Up/Down` | Scroll terminal output one line |
| `Ctrl+C` | Interrupt running process |
| `Ctrl+K` | Clear terminal (when focused) |
| `Ctrl+Home/End` | Scroll to top/bottom of terminal buffer |

> **Tip:** Click a terminal in the Terminal panel's dropdown list and press `Ctrl+Shift+\`` to rename it — useful when running multiple services.

---

## Code Navigation

### Go To

| Shortcut | Action |
|----------|--------|
| `F12` | Go to Definition |
| `Ctrl+F12` | Go to Implementation |
| `Shift+F12` | Find All References |
| `Alt+F12` | Peek Definition (inline, without leaving current file) |
| `Ctrl+Shift+F12` | Peek References (inline) |
| `Ctrl+Shift+\` | Jump to matching bracket |
| `Ctrl+Home` | Go to top of file |
| `Ctrl+End` | Go to bottom of file |
| `Ctrl+Up/Down` | Scroll viewport without moving cursor |

### Breadcrumbs & Outline

| Shortcut | Action |
|----------|--------|
| `Ctrl+Shift+.` | Focus Breadcrumbs bar |
| `←/→` while in Breadcrumbs | Navigate up/down the path |
| `Ctrl+Shift+P` → "Open Outline" | Open file outline in sidebar |

---

## Search & Replace

### In Current File

| Shortcut | Action |
|----------|--------|
| `Ctrl+F` | Find in file |
| `Ctrl+H` | Find and Replace in file |
| `F3` | Next match |
| `Shift+F3` | Previous match |
| `Alt+Enter` | Select all matches (while search box is open) |
| `Ctrl+D` | Select current word, then each next occurrence |
| `Ctrl+Shift+L` | Select all occurrences of current selection |
| `Escape` | Close find widget |

### Across Workspace

| Shortcut | Action |
|----------|--------|
| `Ctrl+Shift+F` | Find in all files |
| `Ctrl+Shift+H` | Replace in all files |
| `Alt+Enter` | Open all matches as editor tabs (from search results) |

---

## Multi-Cursor & Selection

Multi-cursor is one of the highest-leverage features in VS Code.

### Adding Cursors

| Shortcut | Action |
|----------|--------|
| `Alt+Click` | Add cursor at click point |
| `Ctrl+Alt+Up` | Add cursor above current line |
| `Ctrl+Alt+Down` | Add cursor below current line |
| `Ctrl+D` | Add cursor at next occurrence of selected word |
| `Ctrl+Shift+L` | Add cursor at ALL occurrences of selected word |
| `Shift+Alt+I` | Add cursor at end of each line in selection |
| `Shift+Alt+Drag` | Column (box) selection |
| `Ctrl+U` | Undo last cursor add |

### Expanding Selection

| Shortcut | Action |
|----------|--------|
| `Ctrl+L` | Select entire current line |
| `Shift+Alt+Right` | Expand selection (smart — by scope) |
| `Shift+Alt+Left` | Shrink selection (smart) |
| `Ctrl+Shift+Right/Left` | Extend selection word by word |

> **Tip:** `Ctrl+D` repeatedly is great for renaming a variable within a local scope without using a full rename refactor.

---

## Code Editing

### Line Operations

| Shortcut | Action |
|----------|--------|
| `Alt+Up` | Move line up |
| `Alt+Down` | Move line down |
| `Shift+Alt+Up` | Duplicate line above |
| `Shift+Alt+Down` | Duplicate line below |
| `Ctrl+Shift+K` | Delete entire line |
| `Ctrl+Enter` | Insert new line below (cursor stays on current line) |
| `Ctrl+Shift+Enter` | Insert new line above |
| `Ctrl+Shift+\` | Jump to matching bracket |

### Indentation & Formatting

| Shortcut | Action |
|----------|--------|
| `Ctrl+]` | Indent line / selection |
| `Ctrl+[` | Outdent line / selection |
| `Shift+Alt+F` | Format entire document |
| `Ctrl+K Ctrl+F` | Format selection only |
| `Ctrl+K Ctrl+X` | Trim trailing whitespace |
| `Tab` / `Shift+Tab` | Indent / outdent (with selection) |

### Comments

| Shortcut | Action |
|----------|--------|
| `Ctrl+/` | Toggle line comment |
| `Shift+Alt+A` | Toggle block comment |

### Refactoring & Quick Actions

| Shortcut | Action |
|----------|--------|
| `F2` | Rename symbol (all references across workspace) |
| `Ctrl+.` | Quick Fix / light bulb (code actions, imports, etc.) |
| `Ctrl+Shift+R` | Refactor menu (extract method, move, etc.) |
| `F8` | Go to next error or warning in file |
| `Shift+F8` | Go to previous error or warning in file |

---

## Code Folding

| Shortcut | Action |
|----------|--------|
| `Ctrl+Shift+[` | Fold (collapse) current region |
| `Ctrl+Shift+]` | Unfold (expand) current region |
| `Ctrl+K Ctrl+[` | Fold all sub-regions |
| `Ctrl+K Ctrl+]` | Unfold all sub-regions |
| `Ctrl+K Ctrl+0` | Fold all regions in file |
| `Ctrl+K Ctrl+J` | Unfold all regions in file |
| `Ctrl+K Ctrl+1` | Fold to level 1 |
| `Ctrl+K Ctrl+2` | Fold to level 2 |
| `Ctrl+K Ctrl+3` | Fold to level 3 |

---

## Integrated Git / Source Control

| Shortcut | Action |
|----------|--------|
| `Ctrl+Shift+G` | Open Source Control panel |
| `Ctrl+Enter` | Commit staged changes (when in commit message box) |
| `Ctrl+Shift+P` → "Stage All" | Stage all changes |
| `Ctrl+Shift+P` → "Git: Sync" | Pull then push |

> **Tip with GitLens installed:**

| Shortcut | Action |
|----------|--------|
| `Ctrl+Shift+G G` | Open GitLens commit graph |
| Hover on a line | Show inline blame with commit info |
| `Ctrl+Shift+P` → "GitLens: Open File History" | Browse a file's commit history |

---

## GitHub Copilot

| Shortcut | Action |
|----------|--------|
| `Tab` | Accept current inline suggestion |
| `Ctrl+Right` | Accept next word of suggestion only |
| `Escape` | Dismiss suggestion |
| `Alt+]` | Show next suggestion |
| `Alt+[` | Show previous suggestion |
| `Ctrl+Enter` | Open Copilot completions panel (all suggestions) |
| `Ctrl+I` | Trigger Copilot inline chat (in editor) |
| `Ctrl+Alt+I` | Open Copilot Chat panel (sidebar) |
| `Ctrl+Shift+P` → "Copilot: Fix This" | Ask Copilot to fix the current error |

---

## Debugging

| Shortcut | Action |
|----------|--------|
| `F5` | Start debugging / Continue |
| `Shift+F5` | Stop debugging |
| `Ctrl+Shift+F5` | Restart debugging |
| `F9` | Toggle breakpoint on current line |
| `Shift+F9` | Toggle inline breakpoint |
| `F10` | Step Over |
| `F11` | Step Into |
| `Shift+F11` | Step Out |
| `Ctrl+Shift+D` | Open Run & Debug panel |
| `Ctrl+Shift+Y` | Open Debug Console |

> **Tip:** `F5` with no launch config will prompt you to create one, or will auto-detect the project type.

---

## Settings & Customization

| Shortcut | Action |
|----------|--------|
| `Ctrl+,` | Open Settings (UI) |
| `Ctrl+Shift+P` → "Open User Settings (JSON)" | Edit `settings.json` directly |
| `Ctrl+K Ctrl+S` | Open Keyboard Shortcuts editor |
| `Ctrl+Shift+P` → "Configure User Snippets" | Create custom code snippets |
| `Ctrl+Shift+P` → "Reopen Editor With" | Change how the current file is rendered |

---

## Useful Patterns (Combinations)

### Rename a local variable without full refactor
1. Double-click the variable to select it
2. `Ctrl+Shift+L` — select all occurrences in file
3. Type the new name — all instances update simultaneously

### Open terminal, run command, close terminal
1. `Ctrl+\`` — open terminal
2. Run your command
3. `Ctrl+J` — collapse the panel without closing the terminal

### Quickly jump between two files
1. `Alt+Left / Alt+Right` — back and forward through navigation history
2. Or `Ctrl+Tab` to cycle open tabs

### Fix all lint errors fast
1. `F8` — jump to first error
2. `Ctrl+.` — open quick fix
3. `Enter` — apply fix
4. Repeat with `F8`

### Multi-line edit with same content
1. Select the lines you want to edit
2. `Shift+Alt+I` — place a cursor at the end of each line
3. Type — all lines get the same suffix

---

## Sources

[1] [VS Code Key Bindings documentation](https://code.visualstudio.com/docs/getstarted/keybindings)  
[2] [VS Code Tips & Tricks](https://code.visualstudio.com/docs/getstarted/tips-and-tricks)  
[3] [Printable keyboard shortcut reference – Windows](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)  
[4] [Printable keyboard shortcut reference – macOS](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)  
[5] [Printable keyboard shortcut reference – Linux](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)
