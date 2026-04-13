# Prompt: Update INDEX.md

Use this prompt after adding one or more new KB entries to keep `INDEX.md` current.

---

## The Prompt

Copy and paste the following, filling in the `[NEW FILES]` section:

---

> I've added the following new entries to my knowledge base:
>
> [NEW FILES — list each file with its path, e.g.:]
> - `environment/docker-compose-260501a.md`
> - `engineering/rest-api-patterns-260502a.md`
>
> Please update my `INDEX.md` by adding rows for each new file to the appropriate category table.
>
> **INDEX.md format:**
> ```markdown
> | [path/filename.md](path/filename.md) | YYYY-MM-DD | `tag1`, `tag2` | One-line summary |
> ```
>
> Rules:
> - Extract the date from the filename (`YYMMDDa` → `YYYY-MM-DD`)
> - Derive tags from the entry's **Tags** header
> - Write a one-line summary based on the entry's **TL;DR** section
> - Place the row in the correct category section (`## environment` or `## engineering`)
> - Also update the **Stats** section at the bottom: increment the total count and the relevant category count, and update "Last updated"
>
> Here is the current `INDEX.md`:
>
> [PASTE CURRENT INDEX.md CONTENT HERE]
>
> And here are the new entries:
>
> [PASTE EACH NEW ENTRY'S CONTENT HERE]

---

## After Receiving the Updated INDEX.md

1. Review the new rows for accuracy
2. Replace the contents of `INDEX.md` with the updated version
3. Commit: `git add INDEX.md && git commit -m "Update INDEX.md: add [entry name]"`
