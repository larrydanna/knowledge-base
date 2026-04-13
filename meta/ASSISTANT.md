# Working with AI Assistants

Practices for getting the most out of AI coding assistants (GitHub Copilot, Claude, ChatGPT, etc.) using this knowledge base.

---

## Starting a Session

### Recommended context to provide at the start of every session

1. **`context-base.md`** (from this repo) — your shared identity, environment, and preferences
2. **`~/HOME.md`** (local, machine-specific) — current machine's tools, install status, active projects
3. **`INDEX.md`** (optional but high-value) — lets the assistant know what KB entries exist and can reference them

**Combining them:**
> Paste `context-base.md` first, then `HOME.md`, then optionally `INDEX.md`. Most assistants handle 3–5 short files easily in a single context window.

For GitHub Copilot in VS Code, you can use `#file` references or open the files in the editor before asking questions.

---

## Creating a New KB Entry

When you learn something worth saving:

1. Ask the assistant to write a new KB entry using the `prompts/new-kb-entry.md` template
2. Review the output — correct any inaccuracies
3. Save the file to the appropriate category folder using the naming convention from `meta/CONVENTIONS.md`
4. Update `INDEX.md` — use `prompts/kb-update.md` or do it manually

> **Rule of thumb:** If you asked an AI the same question twice, it belongs in the knowledge base.

---

## Keeping the KB Current

- **After installing/configuring a tool:** create or update an `environment/` entry
- **After solving a tricky problem:** create an `engineering/` entry with the solution and context
- **After a session where the assistant taught you something:** extract the key insight into a KB entry
- **Monthly:** review INDEX.md for stale or redundant entries; archive by adding `-archived` suffix

---

## Multi-Assistant Tips

This KB is designed to be **assistant-agnostic**. The same files work with:

| Assistant | How to provide context |
|-----------|----------------------|
| **GitHub Copilot (VS Code)** | Open `context-base.md` + `HOME.md` in editor; use `#file` in chat or Copilot will pick them up via workspace context |
| **GitHub Copilot CLI** | Paste content of `context-base.md` + `HOME.md` into your first message |
| **Claude (claude.ai)** | Use "Add content" / file upload, or paste directly |
| **ChatGPT** | Paste into the first message, or use a GPT with file upload |

### What NOT to paste into a session
- Full KB entries (paste `INDEX.md` instead — the assistant can ask for specific entries if needed)
- Binary files, screenshots, or very long logs (summarize first)
- Secrets, API keys, or credentials (never)

---

## Prompt Engineering Tips

- **Be specific about your environment:** "On Windows 11, PowerShell 7" is more useful than "on my machine"
- **Reference KB entries by name:** "See `environment/wsl-260413a.md` for context" — the assistant can use this as an anchor
- **Ask for KB-formatted output:** "Write your answer as a KB entry following `meta/CONVENTIONS.md`"
- **Cite your work:** When an assistant provides an answer you're saving, ask it to include sources

---

## Session End Checklist

- [ ] Did I learn anything worth saving? → Create a KB entry
- [ ] Did any tool installs succeed/fail? → Update `~/HOME.md`
- [ ] Did INDEX.md need updating? → Run `prompts/kb-update.md`
- [ ] Did any existing KB entries become outdated? → Update them
