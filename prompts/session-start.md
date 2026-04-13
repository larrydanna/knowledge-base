# Prompt: Session Start

Use this to prime any AI assistant at the beginning of a new session.

---

## Option A — Quick Start (paste two files)

1. Paste the contents of `context-base.md`
2. Paste the contents of `~/HOME.md`
3. Add this line:

> "That's my context. Please acknowledge what you now know about my environment and let me know you're ready."

---

## Option B — Full Context (paste three files)

Same as Option A, plus paste `INDEX.md`, then add:

> "That's my context, including my knowledge base index. If I reference a KB entry by filename, you can assume you should treat it as authoritative context for that topic. Ready to start."

---

## Option C — Minimal (single prompt)

If you don't want to paste files, use this standalone prompt:

---

> I'm a developer working on **Windows 11** using **PowerShell** as my primary shell and **VS Code** with GitHub Copilot as my editor. I also use GitHub CLI (`gh`) and Git installed via winget.
>
> **My preferences:**
> - Concise answers — lead with the answer, then explain
> - PowerShell-first for all command-line instructions (not bash/cmd unless I ask)
> - Code blocks for all commands and code
> - No global npm installs without asking
>
> **What I'm working on today:** [describe your task or goal]
>
> Please confirm you understand my environment and are ready to help.

---

## Tips

- Re-paste `~/HOME.md` at the start of a new session if your install status has changed recently
- If the assistant starts giving Linux/bash answers, remind it: *"I'm on Windows/PowerShell — please adjust"*
- For long sessions, periodically remind the assistant of key constraints (it can lose context)
