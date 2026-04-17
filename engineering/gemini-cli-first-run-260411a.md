# Gemini CLI

**Date:** 2026-04-11  
**Category:** engineering  
**Tags:** `gemini`, `cli`, `workflow`, `customization`  
**Related:** [gemini-cli-install-260411a.md](../environment/gemini-cli-install-260411a.md)

---

## TL;DR

- Gemini CLI v0.37.1 displays authentication status and plan on startup
- Supports GEMINI.md files for workspace-specific customization
- Shift+Tab to accept edits, ? for shortcuts
- Can operate in sandbox mode with model selection

---

## Hello, Gemini

This is the first screen on my display. 4/12/2026, 1:16:15 PM

```
 ▝▜▄     Gemini CLI v0.37.1
   ▝▜▄
  ▗▟▀    Signed in with Google /auth
 ▝▀      Plan: Gemini Code Assist for individuals /upgrade

╭──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ We're making changes to Gemini CLI that may impact your workflow.                                                                                                    │
│ What's Changing: We are adding more robust detection of policy-violating use cases and restricting models for free tier users.                                       │
│ How it affects you: If you need use of Gemini pro models you will need to upgrade to a supported paid plan.                                                          │
│ Read more: https://goo.gle/geminicli-updates                                                                                                                         │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯

Tips for getting started:
1. Create GEMINI.md files to customize your interactions
2. /help for more information
3. Ask coding questions, edit code or run commands
4. Be specific for the best results


                                                                                                                                                        ? for shortcuts
────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
 Shift+Tab to accept edits
▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀
 >   Type your message or @path/to/file
▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
 workspace (/directory)                                                        sandbox                                                                           /model
 ~                                                                             no sandbox                                                        gemini-3-flash-preview
 ```

---

## First Chat Request

My first chat request. Very interesting.

>[!NOTE]
>There's some oddly specific references to `Commodore 64` and `Playwright`.

```
 > Make a plan for an initial GEMINI.md in this folder.
▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
✦ I will start by researching the purpose and recommended structure of a GEMINI.md file using the cli_help tool.

╭──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ ≡ Agent Completed (ctrl+o to expand)                                                                                                                             │
│ ✓ cli_help · Completed successfully                                                                                                                              │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯

✦ I will read the KnowledgeBase.md and .brain/Brain-Folder-Notes-260411a.md files to gather more context about the user's preferences and the nature of this workspace.

╭──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ ✓  ReadFile KnowledgeBase.md                                                                                                                                     │
│                                                                                                                                                                  │
│                                                                                                                                                                  │
│ ✓  ReadFile .\...\Brain-Folder-Notes-260411a.md                                                                                                                  │
│                                                                                                                                                                  │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯

✦ I will check for the existence and content of .brain/memory.json to see if there is any additional persistent context that should be included or referenced in the
  GEMINI.md file.

╭──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ ✓  ReadFile .brain\memory.json                                                                                                                                   │
│                                                                                                                                                                  │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯

✦ I have analyzed the current workspace and the existing documentation (KnowledgeBase.md, .brain/, etc.). I propose the following strategy for the GEMINI.md file:

  Proposed Strategy for GEMINI.md

   1. Persona & Context: Establish Gemini CLI as a senior AI collaborator for Larry's AI Research and Development hub. This directory is a central workspace for
      multiple AI-assisted coding tools (Claude, Copilot, Codex, Gemini) and diverse development projects (.NET/C#, Commodore 64).
   2. Contextual Awareness:
       * Knowledge Hub: Instruct the model to treat KnowledgeBase.md as the primary index for project-wide learning and documentation.
       * Persistent Memory: Explicitly reference the .brain/ folder (specifically memory.json) for cross-session context, architectural rules, and user preferences.
       * User Profile: Identify the user as Larry (github.username: larrydanna).
   3. Operational Directives:
       * Tone: Maintain a senior-level, concise, and direct professional tone.
       * Structure: Be mindful of the high-level organization (e.g., source/ for code, kb/ for knowledge, and various .tool/ folders for configuration).
       * Project-Specific Rules: Prioritize local context (found in GEMINI.md files or KnowledgeBase.md) over general AI assumptions.
   4. Specializations:
       * Recognize and support development in .NET (Playwright, xUnit) and retro-computing (Commodore 64).
       * Stay aligned with the user's "Home Folder Practices" and learning goals (e.g., Playwright).

  Does this strategy look good to you, or would you like to add/modify any specific instructions?


                                                                                                                                                        ? for shortcuts
────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
 plan Shift+Tab to manual
▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀
 >   Type your message or @path/to/file
▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
 workspace (/directory)                                                        sandbox                                                                           /model
 ~                                                                             no sandbox                                                        gemini-3-flash-preview
 ```

---

## Plan: Initial GEMINI.md for Workspace Context

### Objective
Create an initial `GEMINI.md` file in the root directory (`C:\Users\larry\`) to provide persistent, project-specific context and instructional guidance for the Gemini CLI. This file will align Gemini's behavior with the user's established workflows, documentation practices, and development focus.

### Key Files & Context
- **Knowledge Base**: `KnowledgeBase.md` acts as the central index for project-wide learning and documentation.
- **Persistent Memory**: The `.brain/` folder (specifically `memory.json`) stores user identity and cross-session context.
- **Workspace Structure**: A multi-tool R&D hub involving Gemini, Claude, Codex, and Copilot, with diverse projects (e.g., .NET, Commodore 64).

### Proposed Content for `GEMINI.md`
```markdown
# Workspace: Larry's AI R&D Hub

## Persona & Collaboration
- You are a senior AI collaborator assisting Larry (`github.username: larrydanna`) in a high-velocity R&D environment.
- Maintain a professional, direct, and senior-level tone. Prioritize technical rationale and concise implementation.

## Contextual Awareness
- **Knowledge Base**: Treat `KnowledgeBase.md` as the primary index for project-wide learning, documentation, and "lessons learned."
- **Persistent Memory**: Reference `.brain/memory.json` for persistent user context and cross-session preferences.
- **Project Structure**:
  - `source/`: Primary directory for development projects.
  - `kb/`: Supporting knowledge base files and tutorials.
  - `.brain/`: Persistent memory and architectural rules.
  - `.claude/`, `.codex/`, `.gemini/`, etc.: Tool-specific configuration and state.

## Operational Directives
- **Conventions**: Adhere to existing styles in `KnowledgeBase.md` and project-specific `GEMINI.md` files (if present in subdirectories).
- **Learning Goals**: Be proactive in supporting active learning paths, such as Playwright and .NET development.
- **Retro-Computing**: Provide specialized support for Commodore 64 development and related tools (e.g., DirMaster, KickAss-C64).

## Technical Standards
- Prioritize clean abstractions and idiomatic code (C#, PowerShell, Markdown).
- For bug fixes, always attempt to reproduce the issue before applying a fix.
- Ensure all documentation uses GitHub-compliant Markdown with appropriate alerts and formatting.
```

### Implementation Steps
1. Create the `GEMINI.md` file at `C:\Users\larry\GEMINI.md` with the content defined above.

### Verification
1. Verify the file exists in the root directory.
2. Run `/memory show` (conceptually, as the model) to ensure the context is correctly loaded by the CLI in subsequent turns.
