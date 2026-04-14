# Knowledge Base

A personal living knowledge base for software development — designed to be used alongside AI coding assistants (GitHub Copilot, Claude, ChatGPT, etc.).

---

## What's in here

| Path | Purpose |
|------|---------|
| `INDEX.md` | Master index of all entries — paste into any AI session |
| `context-base.md` | Shared identity/preferences — paste at the start of any AI session |
| `environment/` | Dev environment entries: tools, installs, configs |
| `engineering/` | Software engineering entries: languages, patterns, frameworks |
| `meta/CONVENTIONS.md` | How to write and name KB entries |
| `meta/ASSISTANT.md` | How to work with AI assistants using this KB |
| `meta/ORIGIN.md` | How this knowledge base came to be |
| `prompts/` | Reusable AI prompt templates |

---

## Quick Start on a New Machine

```powershell
# Clone the repo to your home directory
git clone https://github.com/[YOUR-USERNAME]/knowledge-base "$HOME\knowledge-base"

# Open it in VS Code
code "$HOME\knowledge-base"
```

Then:
1. Update `context-base.md` if your role or preferences have changed
2. Create a new `~/HOME.md` for this machine (see the template section in `meta/ASSISTANT.md`)
3. Check `INDEX.md` to see what knowledge is already available

---

## Starting an AI Session

For the best results with any AI assistant:

1. Paste `context-base.md` (shared preferences and identity)
2. Paste `~/HOME.md` (this machine's tools and current status)
3. Optionally paste `INDEX.md` (so the assistant knows what KB entries exist)

See `meta/ASSISTANT.md` for detailed guidance per assistant type.

---

## Adding a New Entry

1. Pick the right category folder (`environment/` or `engineering/`)
2. Name the file: `kebab-topic-YYMMDDa.md` (see `meta/CONVENTIONS.md`)
3. Use the entry template from `meta/CONVENTIONS.md`
4. Update `INDEX.md` with the new entry
5. Commit and push

> **Shortcut:** Use `prompts/new-kb-entry.md` to have an AI write the entry for you.

---

## File Naming

```
kebab-topic-YYMMDDa.md
```
Example: `docker-compose-basics-260501a.md` — created May 1, 2026, first entry of the day on this topic.

---

## Git Workflow

This repo is intentionally simple — no branches, no PRs. Just commit to `master` as you work.

```powershell
git add -A
git commit -m "Add entry: topic summary"
git push
```

**What's NOT in this repo:**
- `~/HOME.md` — machine-specific, lives outside the repo
- `*.local.md` — any file you want to keep local (gitignored)
