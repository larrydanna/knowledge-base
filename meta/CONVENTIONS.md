# Knowledge Base Conventions

This document defines the standards for all entries in this knowledge base.  
**It is intentionally AI-readable** — an assistant can follow these rules to auto-format new entries.

---

## File Naming

```
kebab-topic-YYMMDDa.md
```

- **`kebab-topic`** — lowercase, hyphen-separated description of the subject (e.g., `git-via-winget`, `react-hooks-intro`)
- **`YYMMDD`** — date the entry was created (e.g., `260413` = April 13, 2026)
- **`a`** — revision letter, starting at `a`; increment to `b`, `c`… for same-day revisions on the same topic

**Examples:**
- `node-install-260413a.md`
- `react-hooks-260501a.md`
- `react-hooks-260501b.md` ← same day, revised entry

---

## Categories (Folders)

| Folder | Contents |
|--------|----------|
| `environment/` | Dev machine setup: OS, tools, shell, configs |
| `engineering/` | Software concepts: languages, patterns, frameworks, tools |
| `meta/` | This system: conventions, practices (not indexed in INDEX.md) |
| `prompts/` | Reusable AI prompt templates (not indexed in INDEX.md) |

---

## Entry Template

Every knowledge base entry follows this structure:

```markdown
# [Title]

**Date:** YYYY-MM-DD  
**Category:** environment | engineering  
**Tags:** `tag1`, `tag2`, `tag3`  
**Related:** [Article Title Here](../path/other-entry.md)

---

## TL;DR

- Bullet 1 — the key command or concept
- Bullet 2
- Bullet 3 (max 5 bullets)

---

## [Section Heading]

Body content: steps, commands, explanations.

Use fenced code blocks for all commands:

    ```powershell
    some-command --flag value
    ```

---

## Sources

[1] [Title](https://url)
[2] [Title](https://url)
```

### Rules
- The **TL;DR section is mandatory** — it should be self-contained enough for an AI to extract the key insight without reading the full body
- **Tags** should be 2–6 lowercase single-word or hyphenated terms
- **Related** links are optional but encouraged when entries cover adjacent topics
- **Use article titles in link text**, not file names — e.g., `[GitHub Alerts](path.md)` not `[markdown-alerts-260411a.md](path.md)`
- Keep entries **focused on one topic** — create a new file rather than expanding an existing one into multiple topics
- Prefer **imperative headings** for procedures (e.g., `## Install via winget`) and **noun headings** for reference (e.g., `## Common Post-Install Tips`)

---

## Updating INDEX.md

After adding a new entry, add a row to `INDEX.md` in the appropriate category table:

```
| [environment/my-topic-260413a.md](environment/my-topic-260413a.md) | 2026-04-13 | `tag1`, `tag2` | One-line summary of what this entry covers |
```

Then update the **Stats** section at the bottom of INDEX.md.

> **Tip:** Use the `prompts/kb-update.md` prompt to have an AI assistant update INDEX.md for you.
