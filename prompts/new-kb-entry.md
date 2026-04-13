# Prompt: Generate a New KB Entry

Use this prompt to ask an AI assistant to write a new knowledge base entry.

---

## The Prompt

Copy and paste the following, filling in `[TOPIC]` and optionally `[CONTEXT]`:

---

> Please write a knowledge base entry about **[TOPIC]** for my personal knowledge base.
>
> Follow this format exactly (from my `meta/CONVENTIONS.md`):
>
> **Filename suggestion:** `kebab-topic-YYMMDDa.md` (suggest an appropriate name)
>
> **Structure required:**
> ```
> # [Title]
>
> **Date:** [today's date]
> **Category:** environment | engineering
> **Tags:** `tag1`, `tag2`, `tag3`
> **Related:** (if applicable)
>
> ---
>
> ## TL;DR
>
> - [2-5 bullet points summarizing the key takeaway or command]
>
> ---
>
> ## [Relevant Sections]
>
> [Body content with code blocks, steps, explanations]
>
> ---
>
> ## Sources
>
> [Numbered citations with links]
> ```
>
> **Rules:**
> - TL;DR must be self-contained — someone should get the key insight from bullets alone
> - All commands in fenced code blocks with the appropriate language tag (e.g., ` ```powershell `)
> - My environment is **Windows 11 / PowerShell** — tailor all commands accordingly unless I specify otherwise
> - Be accurate; prefer official documentation as sources
>
> **Additional context:** [CONTEXT — e.g., "I just installed X using winget and ran into issue Y"]

---

## After Receiving the Entry

1. Review for accuracy — especially commands and version numbers
2. Save to the appropriate folder (`environment/` or `engineering/`)
3. Update `INDEX.md` — use `prompts/kb-update.md` or add the row manually
4. Commit: `git add -A && git commit -m "Add entry: [brief description]"`
