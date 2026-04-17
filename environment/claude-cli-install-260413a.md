# Install Claude Code CLI

**Date:** 2026-04-13  
**Category:** environment  
**Tags:** `claude`, `claude-code`, `cli`, `install`, `npm`  
**Related:** [Node](../environment/Node-260413a.md)

---

## TL;DR

- Requires Node.js 18+
- Install globally: `npm install -g @anthropic-ai/claude-code`
- Launch: `claude`
- Authenticate on first run via browser (Anthropic account) or API key

---

## Prerequisites

Node.js 18 or higher must be installed. Verify with:

```powershell
node -v
```

If Node is missing, see [Node-260413a.md](../environment/Node-260413a.md).

---

## Install via npm

```powershell
npm install -g @anthropic-ai/claude-code
```

Verify the installation:

```powershell
claude --version
```

---

## First-Run Authentication

On first launch, run:

```powershell
claude
```

Claude Code will open a browser window to authenticate with your Anthropic account. Alternatively, set an API key directly:

```powershell
$env:ANTHROPIC_API_KEY = "sk-ant-..."
claude
```

To persist the key across sessions, add it to your PowerShell profile or system environment variables.

---

## Common Post-Install Tips

- Run `claude update` to upgrade to the latest version.
- Use `claude --help` to see available flags and commands.
- Run `claude doctor` to diagnose configuration issues.

---

## Sources

[1] [Claude Code Quickstart](https://docs.anthropic.com/en/docs/claude-code/quickstart)  
[2] [Claude Code Overview](https://docs.anthropic.com/en/docs/claude-code/overview)
