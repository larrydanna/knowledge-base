# Workstation Setup — macOS

**Date:** 2026-04-13  
**Category:** environment  
**Tags:** `macos`, `setup`, `onboarding`, `homebrew`, `dotnet`, `vscode`  
**Related:** [Node](Node-260413a.md) · [Install Claude Code CLI](claude-cli-install-260413a.md) · [Workstation Setup — Windows 10 / 11](workstation-setup-windows-260413a.md)

> **Living document** — add tools as they come up. The order below reflects dependencies: install phases in sequence, but within a phase order is flexible.

---

## TL;DR

Install in this order:

1. Xcode Command Line Tools
2. Homebrew
3. Git (via Homebrew)
4. GitHub CLI (`gh`)
5. VS Code
6. nvm → Node.js LTS
7. .NET SDK
8. Azure CLI
9. Docker Desktop
10. Claude Code CLI (`npm i -g @anthropic-ai/claude-code`)
11. VS Code extensions (Copilot, C#, etc.)

---

## Phase 1 — Xcode Command Line Tools

Required before anything else — provides `git`, `make`, compilers, and SDK headers:

```bash
xcode-select --install
```

A dialog will prompt you to install. Confirm and wait for completion. Verify:

```bash
xcode-select -p
# Expected: /Library/Developer/CommandLineTools
```

---

## Phase 2 — Package Manager (Homebrew)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

On **Apple Silicon (M-series)** Homebrew installs to `/opt/homebrew`. Add it to your PATH:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

On **Intel Macs** Homebrew installs to `/usr/local` and PATH is set automatically.

Verify:

```bash
brew --version
brew doctor
```

---

## Phase 3 — Version Control

### Git

macOS ships with an older Apple Git. Install the Homebrew version:

```bash
brew install git
```

Configure identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global core.autocrlf input
```

### GitHub CLI

```bash
brew install gh
```

Authenticate:

```bash
gh auth login
```

Choose **GitHub.com → HTTPS → Login with browser**.

---

## Phase 4 — Shell (Optional Enhancements)

macOS defaults to **zsh**. Optionally enhance it:

```bash
# Oh My Zsh (themes, plugins, git prompt)
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### PowerShell 7 (for cross-platform consistency)

```bash
brew install --cask powershell
```

Verify:

```bash
pwsh --version
```

---

## Phase 5 — Editor

### VS Code

```bash
brew install --cask visual-studio-code
```

Verify the `code` command works (VS Code auto-installs the shell command):

```bash
code --version
```

### Core Extensions

```bash
code --install-extension GitHub.copilot
code --install-extension GitHub.copilot-chat
code --install-extension ms-dotnettools.csharp
code --install-extension ms-dotnettools.csdevkit
code --install-extension eamodio.gitlens
code --install-extension PKief.material-icon-theme
code --install-extension kejun.markdown-alert

# GitHub Flavored Markdown preview (see vscode-gfm-markdown-260413a.md)
code --install-extension bierner.github-markdown-preview
```

---

## Phase 6 — Runtimes

### Node.js (via nvm)

See: [Node-260413a.md](Node-260413a.md)

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash
# Restart terminal, then:
nvm install --lts
nvm use --lts
node -v && npm -v
```

### .NET SDK

```bash
brew install --cask dotnet-sdk
```

Or install a specific version:

```bash
brew install dotnet@8
```

Verify:

```bash
dotnet --version
dotnet --list-sdks
```

> On Apple Silicon, .NET 6+ has native ARM64 support.

---

## Phase 7 — Cloud & DevOps

### Azure CLI

```bash
brew install azure-cli
```

Sign in:

```bash
az login
```

### Azure DevOps Extension (optional)

```bash
az extension add --name azure-devops
az devops configure --defaults organization=https://dev.azure.com/YOUR-ORG
```

---

## Phase 8 — Containers

### Docker Desktop

```bash
brew install --cask docker
```

Open Docker Desktop from Applications to complete first-run setup.

Verify (after Docker Desktop is running):

```bash
docker --version
docker run hello-world
```

---

## Phase 9 — AI Coding Assistants

### GitHub Copilot

Installed via VS Code extensions in Phase 5. Sign in through VS Code's Accounts menu.

### Claude Code CLI

Requires Node.js (Phase 6). See: [claude-cli-install-260413a.md](claude-cli-install-260413a.md)

```bash
npm install -g @anthropic-ai/claude-code
claude
```

---

## Clone Personal Repos

```bash
gh repo clone YOUR-USERNAME/knowledge-base "$HOME/knowledge-base"
```

---

## Sources

[1] [Homebrew](https://brew.sh)  
[2] [GitHub CLI – Homebrew](https://cli.github.com)  
[3] [.NET on macOS – Microsoft](https://learn.microsoft.com/en-us/dotnet/core/install/macos)  
[4] [Azure CLI on macOS – Microsoft](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-macos)  
[5] [Docker Desktop for Mac](https://docs.docker.com/desktop/install/mac-install/)  
[6] [Oh My Zsh](https://ohmyz.sh)
