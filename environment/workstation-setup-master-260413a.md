# Workstation Setup — Master Guide

**Date:** 2026-04-13  
**Category:** environment  
**Tags:** `setup`, `onboarding`, `windows`, `ubuntu`, `macos`, `cross-platform`  
**Related:** [workstation-setup-windows-260413a.md](workstation-setup-windows-260413a.md) · [workstation-setup-ubuntu-260413a.md](workstation-setup-ubuntu-260413a.md) · [workstation-setup-macos-260413a.md](workstation-setup-macos-260413a.md)

> **Living document.** This is the starting point for any new dev workstation. Pick your OS and follow its article — this guide covers the common toolset, install philosophy, and cross-platform notes.

---

## TL;DR

- **Pick your OS article** and follow the phases in order — phases reflect dependency order, not priority
- Every platform gets the same logical toolset; only the package manager and some commands differ
- Install runtimes via a **version manager** (nvm, etc.), not system package managers, for flexibility
- AI coding assistants (Copilot, Claude) go in **last** — they depend on Node and the editor

---

## OS-Specific Articles

| OS | Article |
|----|---------|
| Windows 10 / 11 | [workstation-setup-windows-260413a.md](workstation-setup-windows-260413a.md) |
| Ubuntu / Linux | [workstation-setup-ubuntu-260413a.md](workstation-setup-ubuntu-260413a.md) |
| macOS | [workstation-setup-macos-260413a.md](workstation-setup-macos-260413a.md) |

---

## Universal Toolset

The same logical set of tools on every platform — only the installer differs.

| Phase | Tool | Windows | Ubuntu | macOS |
|-------|------|---------|--------|-------|
| 1 | Package manager | winget | apt | Homebrew |
| 2 | Shell | PowerShell 7 | PowerShell 7 / bash | zsh + PowerShell 7 |
| 3 | Version control | Git + gh | Git + gh | Git + gh |
| 4 | Editor | VS Code | VS Code | VS Code |
| 5 | JS runtime | nvm-windows → Node LTS | nvm → Node LTS | nvm → Node LTS |
| 5 | .NET runtime | dotnet SDK 8 | dotnet SDK 8 | dotnet SDK 8 |
| 6 | Cloud CLI | Azure CLI + DevOps ext | Azure CLI + DevOps ext | Azure CLI + DevOps ext |
| 7 | Linux layer | WSL 2 + Ubuntu | *(native)* | *(not applicable)* |
| 7 | Containers | Docker Desktop | Docker Engine | Docker Desktop |
| 8 | AI assistant – editor | GitHub Copilot (ext) | GitHub Copilot (ext) | GitHub Copilot (ext) |
| 8 | AI assistant – CLI | Claude Code (`npm`) | Claude Code (`npm`) | Claude Code (`npm`) |

---

## Install Philosophy

### Install phases in order — within a phase, order is flexible

Dependencies flow downward:

```
Package manager
  └── Shell / terminal
        └── Git + GitHub CLI
              └── Editor + extensions
                    └── Runtimes (Node, .NET)
                          └── Cloud & DevOps tools
                                └── Containers
                                      └── AI coding assistants
```

### Use version managers for runtimes

Avoid installing Node.js or Python directly from system package managers — they make version switching painful and often require `sudo` for global packages.

| Runtime | Windows | Ubuntu / macOS |
|---------|---------|----------------|
| Node.js | nvm-windows | nvm |
| Python | pyenv-win | pyenv |
| Ruby | *(add when needed)* | rbenv |
| Java | *(add when needed)* | SDKMAN |

### Use `winget` / `brew` / `apt` for everything else

For tools that don't need version management — Git, VS Code, Azure CLI, Docker — always prefer the system package manager over manual downloads. It makes updates and reinstalls reproducible.

---

## Cross-Platform Notes

### PowerShell everywhere

PowerShell 7 is available on all three platforms and recommended for scripting consistency. On Windows it coexists with PowerShell 5.1 (do not remove 5.1).

```bash
# Check version on any platform
pwsh --version
```

### Git line endings

| Platform | Recommended setting |
|----------|-------------------|
| Windows | `core.autocrlf = true` |
| Ubuntu / macOS | `core.autocrlf = input` |

### SSH keys

After setting up Git and `gh`, generate an SSH key and add it to GitHub:

```bash
ssh-keygen -t ed25519 -C "you@example.com"
gh ssh-key add ~/.ssh/id_ed25519.pub --title "hostname-date"
```

On Windows, the key path is `~/.ssh/id_ed25519.pub` in both PowerShell and WSL.

### VS Code extensions — install from the CLI

All OS articles include the same `code --install-extension` commands. This list is the minimum; add project-specific extensions per-repo via `.vscode/extensions.json`.

**Baseline extensions:**

| Extension ID | Purpose |
|---|---|
| `GitHub.copilot` | AI completions |
| `GitHub.copilot-chat` | AI chat panel |
| `ms-dotnettools.csharp` | C# language support |
| `ms-dotnettools.csdevkit` | C# dev kit (test runner, solution explorer) |
| `eamodio.gitlens` | Git history and blame |
| `PKief.material-icon-theme` | File icon theme |

---

## First Actions After Setup

Once the toolset is installed, do these before starting project work:

1. **Clone personal repos**
   ```bash
   gh repo clone YOUR-USERNAME/knowledge-base
   ```

2. **Configure Git identity** (if not done during Git install)
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```

3. **Sign in to GitHub Copilot** — VS Code → Accounts menu → Sign in with GitHub

4. **Authenticate Claude Code CLI**
   ```bash
   claude
   # Follows browser-based auth on first run
   ```

5. **Create `~/HOME.md`** — document this machine's name, OS version, installed tools, and any quirks. Keep it outside the repo (it's machine-specific and gitignored).

---

## What's Not Covered Here

These are intentionally omitted — add entries to the KB as they come up:

- Language-specific toolchains beyond Node and .NET (Python, Java, Go, Rust…)
- Database clients (SSMS, pgAdmin, DBeaver…)
- Browser dev tools and extensions
- Team / project-specific tooling
- VPN and remote access
- Hardware-specific drivers and peripherals

---

## Sources

See sources in each OS-specific article.
