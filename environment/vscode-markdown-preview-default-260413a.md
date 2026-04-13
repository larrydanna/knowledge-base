# VSCode: Set Markdown Preview as Default

**Date:** 2026-04-13  
**Category:** environment  
**Tags:** `vscode`, `markdown`, `preview`, `settings`, `editor`  
**Related:** *(none)*

---

## TL;DR

- Open a `.md` file → press `Ctrl+Shift+P` → run **"Markdown: Open Preview to the Side"** for a one-off preview
- To always open `.md` files directly in preview mode, install the **Markdown Preview Enhanced** extension and set `"workbench.editorAssociations"` in `settings.json`
- Built-in VSCode cannot open preview as the *sole* default view — use the workaround below or an extension

---

## Open Preview to the Side (One-off)

The quickest way to view rendered Markdown alongside the editor:

1. Open any `.md` file
2. Press `Ctrl+Shift+P` and run **Markdown: Open Preview to the Side**  
   — or click the preview icon (split-pane) in the top-right of the editor tab

```
Keyboard shortcut: Ctrl+K V
```

---

## Set Markdown Files to Always Open in Preview

VSCode's built-in Markdown preview cannot be set as the exclusive default opener via settings alone, but you can configure it to open preview automatically using `settings.json`:

1. Open the Command Palette: `Ctrl+Shift+P`
2. Run **Preferences: Open User Settings (JSON)**
3. Add the following:

```json
"workbench.editorAssociations": {
    "*.md": "vscode.markdown.preview.editor"
}
```

This makes every `.md` file open directly in the built-in preview instead of the raw editor.

> **Note:** To edit the file again, right-click the tab → **Reopen Editor With…** → **Text Editor**.

---

## Reopen as Editor When Needed

When preview is the default, switch back to source editing:

- Right-click the editor tab → **Reopen Editor With…** → **Text Editor**  
- Or use `Ctrl+Shift+P` → **Reopen Editor With**

---

## Sources

[1] [VSCode Markdown Documentation](https://code.visualstudio.com/docs/languages/markdown)  
[2] [workbench.editorAssociations setting – VSCode docs](https://code.visualstudio.com/docs/getstarted/settings)
