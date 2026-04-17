# Workstation Setup — Windows 10 / 11

**Date:** 2026-04-13  
**Category:** environment  
**Tags:** `windows`, `setup`, `onboarding`, `winget`, `dotnet`, `vscode`  
**Related:** [Install Git](git-via-winget-260413a.md) · [WSL](wsl-260413a.md) · [Node](Node-260413a.md) · [Install Claude Code CLI](claude-cli-install-260413a.md)

> **Living document** — add tools as they come up. The order below reflects dependencies: install phases in sequence, but within a phase order is flexible.

---

## TL;DR

Install in this order:

1. winget (confirm or update)
2. Windows Terminal + PowerShell 7
3. Git
4. GitHub CLI (`gh`)
5. VS Code
6. nvm-windows → Node.js LTS
7. .NET SDK
8. Azure CLI
9. WSL 2 + Ubuntu
10. Docker Desktop
11. Claude Code CLI (`npm i -g @anthropic-ai/claude-code`)
12. VS Code extensions (Copilot, C#, etc.)

---

## Phase 1 — Package Manager & Shell

### Confirm winget is available

`winget` ships with Windows 11 by default. On Windows 10 it requires the **App Installer** package from the Microsoft Store (version 1.1+).

```powershell
winget --version
```

If missing on Windows 10, install from the Microsoft Store: search **App Installer**.

### Install Windows Terminal

```powershell
winget install --id Microsoft.WindowsTerminal -e
```

Set as default terminal: Settings → **Default terminal application** → Windows Terminal.

### Install PowerShell 7+

Windows ships with PowerShell 5.1. Install the current stable release:

```powershell
winget install --id Microsoft.PowerShell -e
```

Restart Windows Terminal and confirm:

```powershell
$PSVersionTable.PSVersion
```

---

## Phase 2 — Version Control

### Install Git

```powershell
winget install --id Git.Git -e
```

Configure identity immediately:

```powershell
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global core.autocrlf true
```

### Install GitHub CLI

```powershell
winget install --id GitHub.cli -e
```

Authenticate:

```powershell
gh auth login
```

Choose **GitHub.com → HTTPS → Login with browser**.

---

## Phase 3 — Editor

### Install VS Code

```powershell
winget install --id Microsoft.VisualStudioCode -e
```

Verify the `code` command is in PATH (may require a new terminal session):

```powershell
code --version
```

### Core Extensions

Install via CLI for repeatability:

```powershell
# GitHub Copilot
code --install-extension GitHub.copilot
code --install-extension GitHub.copilot-chat

# C# / .NET
code --install-extension ms-dotnettools.csharp
code --install-extension ms-dotnettools.csdevkit

# General utility
code --install-extension eamodio.gitlens
code --install-extension PKief.material-icon-theme

# Markdown authoring
code --install-extension kejun.markdown-alert

# GitHub Flavored Markdown preview (see vscode-gfm-markdown-260413a.md)
code --install-extension bierner.github-markdown-preview
```

---

## Phase 4 — Runtimes

### Node.js (via nvm-windows)

See: [Node-260413a.md](Node-260413a.md)

```powershell
# After installing nvm-windows from https://github.com/coreybutler/nvm-windows
nvm install lts
nvm use lts
node -v && npm -v
```

### .NET SDK

Install the current LTS SDK:

```powershell
winget install --id Microsoft.DotNet.SDK.8 -e
```

Verify:

```powershell
dotnet --version
dotnet --list-sdks
```

> Add newer SDK entries (e.g., `.SDK.9`) as they become relevant.

---

## Phase 5 — Cloud & DevOps

### Azure CLI

```powershell
winget install --id Microsoft.AzureCLI -e
```

Sign in:

```powershell
az login
```

### Azure DevOps Extension (optional)

```powershell
az extension add --name azure-devops
az devops configure --defaults organization=https://dev.azure.com/YOUR-ORG
```

---

## Phase 6 — Linux Subsystem

### WSL 2 + Ubuntu

See: [wsl-260413a.md](wsl-260413a.md)

```powershell
wsl --install
# Reboot, then complete Ubuntu setup
wsl --set-default-version 2
```

---

## Phase 7 — Containers

### Docker Desktop

Requires WSL 2 to be installed first.

```powershell
winget install --id Docker.DockerDesktop -e
```

After install, open Docker Desktop and enable **Use WSL 2 based engine** in Settings.

Verify:

```powershell
docker --version
docker run hello-world
```

---

## Phase 8 — AI Coding Assistants

### GitHub Copilot

Installed via VS Code extension in Phase 3. Sign in through VS Code's Accounts menu using your GitHub account.

### Claude Code CLI

Requires Node.js (Phase 4). See: [claude-cli-install-260413a.md](claude-cli-install-260413a.md)

```powershell
npm install -g @anthropic-ai/claude-code
claude
```

---

## Clone Personal Repos

Once Git and `gh` are configured:

```powershell
gh repo clone YOUR-USERNAME/knowledge-base "$HOME\knowledge-base"
```

Add other repos as needed.

---

## Sources

[1] [winget documentation – Microsoft](https://learn.microsoft.com/en-us/windows/package-manager/winget/)  
[2] [Windows Terminal – Microsoft](https://learn.microsoft.com/en-us/windows/terminal/)  
[3] [PowerShell releases – GitHub](https://github.com/PowerShell/PowerShell/releases)  
[4] [.NET SDK downloads](https://dotnet.microsoft.com/en-us/download)  
[5] [Azure CLI install – Microsoft](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-windows)  
[6] [Docker Desktop for Windows](https://docs.docker.com/desktop/install/windows-install/)
