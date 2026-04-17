# GitHub Markdown Alerts

**Date:** 2026-04-11  
**Category:** engineering  
**Tags:** `markdown`, `github`, `gfm`, `alerts`, `formatting`  
**Related:** [vscode-gfm-markdown-260413a.md](../environment/vscode-gfm-markdown-260413a.md), [markdown-file-links-260411a.md](markdown-file-links-260411a.md)

---

## TL;DR

- GitHub supports five alert types: NOTE (blue), TIP (green), IMPORTANT (purple), WARNING (yellow), CAUTION (red)
- Syntax: `> [!NOTE]` followed by content in blockquote format
- Also available: `<mark>` tag, blockquotes, code blocks, and diff syntax for highlighting

---

## 1. GitHub Alerts (Recommended)

GitHub recently introduced [official alert syntax](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) to highlight paragraphs with specific colors and icons (Blue, Green, Purple, Yellow, Red). [4] 

> [!NOTE]
> This is a blue-tinted highlight for general information.

> [!TIP]
> This is a green-tinted highlight for helpful advice.

> [!IMPORTANT]
> This is a purple-tinted highlight for critical info.

> [!WARNING]
> This is a yellow-tinted highlight for things to watch out for.

> [!CAUTION]
> This is a red-tinted highlight for negative or dangerous consequences.

---

## 2. The `<mark>` Tag

For a classic "yellow marker" look, [GitHub](https://github.com/) supports the HTML `<mark>` tag. [5, 6] 

<mark>This entire paragraph will have a bright yellow background.</mark>

---

## 3. Blockquotes

For a subtle highlight, use the `>` character. GitHub renders this with a vertical line on the left and grayed text. [7] 

> This is a blockquote. It offsets the paragraph from the rest of the text
> 
> to make it stand out visually.

---

## 4. Code Blocks for Monospacing

If you want a paragraph to have a distinct background box and monospaced font, wrap it in triple backticks. [9, 10] 

```text
This paragraph will be inside a gray box with a monospace font.
```

---

## 5. Diff Syntax (Color Hack)

You can use `diff` syntax to force text to be green or red, which is often used as a workaround for color highlighting.

```diff
+ This text will be highlighted in green (added)
- This text will be highlighted in red (removed)
```

---

## Background

While standard Markdown does not have a native "highlighter" syntax, you can use several [GitHub Flavored Markdown (GFM)](https://github.github.com/gfm/) techniques to highlight paragraphs or specific sections of text: [1, 2] 

---

## Sources

[1] [https://github.com/adam-p/markdown-here/wiki/markdown-cheatsheet](https://github.com/adam-p/markdown-here/wiki/markdown-cheatsheet)
[2] [https://vxlabs.com/2014/04/08/syntax-highlighting-markdown-fenced-code-blocks-in-emacs/](https://vxlabs.com/2014/04/08/syntax-highlighting-markdown-fenced-code-blocks-in-emacs/)
[3] [https://www.doxygen.nl/manual/markdown.html](https://www.doxygen.nl/manual/markdown.html)
[4] [https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
[5] [https://www.reddit.com/r/github/comments/1o72hne/is_there_anyway_to_highlight_text_on_github_md/](https://www.reddit.com/r/github/comments/1o72hne/is_there_anyway_to_highlight_text_on_github_md/)
[6] [https://www.markdownguide.org/extended-syntax/](https://www.markdownguide.org/extended-syntax/)
[7] [https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
[8] [https://www.youtube.com/watch?v=IG9_EM5cw3U](https://www.youtube.com/watch?v=IG9_EM5cw3U)
[9] [https://docs.github.com/enterprise-cloud@latest/contributing/writing-for-github-docs/using-markdown-and-liquid-in-github-docs](https://docs.github.com/enterprise-cloud@latest/contributing/writing-for-github-docs/using-markdown-and-liquid-in-github-docs)
[10] [https://www.online-tech-tips.com/how-to-add-color-to-messages-on-discord/](https://www.online-tech-tips.com/how-to-add-color-to-messages-on-discord/)
