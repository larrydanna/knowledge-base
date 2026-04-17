# How to: Adjust the Indentation of the File Explorer Tree in VS Code

**Date:** 2026-04-11  
**Category:** environment  
**Tags:** `vscode`, `settings`, `ui`, `explorer`, `tree-view`  
**Related:** [VSCode Keyboard Shortcuts — Workflow Reference](vscode-keyboard-shortcuts-260413a.md)

---

## TL;DR

- Set `workbench.tree.indent` to adjust indentation (default: 8, recommended: 16-20)
- Enable indent guides: `workbench.tree.renderIndentGuides: "always"`
- Customize guide color: `tree.indentGuidesStroke` in `workbench.colorCustomizations`

---

## Using the Settings UI

1. Open Settings by pressing `Ctrl + ,` (Windows/Linux) or `Cmd + ,` (macOS).
2. In the search bar, type `tree indent`.
3. Locate **Workbench > Appearance > Tree: Indent**.
4. Change the value (in pixels) to your preference. The default is usually 8, but many users find 16 or 20 much clearer. [1, 2, 3, 4] 

---

## Using settings.json

If you prefer editing the JSON file directly, add this line:

```json
"workbench.tree.indent": 20
```

[1, 5] 

---

## Enhance Visibility with Indent Guides

To make the hierarchy even easier to follow, you can enable vertical lines that connect folders to their contents:

* **Enable Guides**: Search for `tree render indent guides` and set it to `always`.
* **JSON**: `"workbench.tree.renderIndentGuides": "always"`
* **Change Guide Color**: To make these lines stand out, add a custom color to your settings.json:

```json
"workbench.colorCustomizations": {
    "tree.indentGuidesStroke": "#00ff00"
}
```

[1, 8, 9, 10] 

---

## Sources

[1] [https://stackoverflow.com/questions/55310734/how-to-add-more-indentation-in-the-visual-studio-code-explorer-file-tree-structu](https://stackoverflow.com/questions/55310734/how-to-add-more-indentation-in-the-visual-studio-code-explorer-file-tree-structu)
[2] [https://www.ryanchapin.com/vscode-change-indent-for-file-explorer-tree/](https://www.ryanchapin.com/vscode-change-indent-for-file-explorer-tree/)
[3] [https://www.youtube.com/watch?v=3BlwYUjUqyc](https://www.youtube.com/watch?v=3BlwYUjUqyc)
[4] [https://www.youtube.com/watch?v=kGDxv7U4ztg](https://www.youtube.com/watch?v=kGDxv7U4ztg)
[5] [https://stackoverflow.com/questions/55310734/how-to-add-more-indentation-in-the-visual-studio-code-explorer-file-tree-structu/55315106](https://stackoverflow.com/questions/55310734/how-to-add-more-indentation-in-the-visual-studio-code-explorer-file-tree-structu/55315106)
[6] [https://www.youtube.com/watch?v=r3YAY4-BxRo](https://www.youtube.com/watch?v=r3YAY4-BxRo)
[7] [https://betterprogramming.pub/leverage-your-coding-speed-to-the-maximum-with-visual-studio-vscode-shortcuts-and-refactorings-fcbed61b7540](https://betterprogramming.pub/leverage-your-coding-speed-to-the-maximum-with-visual-studio-vscode-shortcuts-and-refactorings-fcbed61b7540)
[8] [https://www.meziantou.net/improve-the-tree-view-settings-in-visual-studio-code.htm](https://www.meziantou.net/improve-the-tree-view-settings-in-visual-studio-code.htm)
[9] [https://www.yellowduck.be/posts/improve-your-vs-code-explorer-file-tree-structure](https://www.yellowduck.be/posts/improve-your-vs-code-explorer-file-tree-structure)
[10] [https://www.reddit.com/r/vscode/comments/1bei260/how_can_i_hide_the_vertical_lines_in_vs_code/](https://www.reddit.com/r/vscode/comments/1bei260/how_can_i_hide_the_vertical_lines_in_vs_code/)
