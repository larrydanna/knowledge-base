# Workstation Setup — Ubuntu (Linux)

**Date:** 2026-04-13  
**Category:** environment  
**Tags:** `ubuntu`, `linux`, `setup`, `onboarding`, `apt`, `dotnet`, `vscode`  
**Related:** [Node-260413a.md](Node-260413a.md) · [claude-cli-install-260413a.md](claude-cli-install-260413a.md) · [workstation-setup-windows-260413a.md](workstation-setup-windows-260413a.md)

> **Living document** — add tools as they come up. The order below reflects dependencies: install phases in sequence, but within a phase order is flexible.

---

## TL;DR

Install in this order:

1. System update + core build tools
2. Git
3. GitHub CLI (`gh`)
4. PowerShell 7 (cross-platform)
5. VS Code
6. nvm → Node.js LTS
7. .NET SDK
8. Azure CLI
9. Docker Engine
10. Claude Code CLI (`npm i -g @anthropic-ai/claude-code`)
11. VS Code extensions (Copilot, C#, etc.)

---

## Phase 1 — System Update & Build Tools

Always start with a full update and essential build dependencies:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl wget git build-essential ca-certificates gnupg lsb-release
```

---

## Phase 2 — Version Control

### Git

Usually already installed. Confirm or install:

```bash
git --version
# or
sudo apt install -y git
```

Configure identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global core.autocrlf input
```

### GitHub CLI

```bash
type -p curl >/dev/null || (sudo apt update && sudo apt install curl -y)
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg \
  | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] \
  https://cli.github.com/packages stable main" \
  | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update && sudo apt install -y gh
```

Authenticate:

```bash
gh auth login
```

---

## Phase 3 — Shell

### PowerShell 7 (optional but consistent with Windows workflow)

```bash
# Via snap (easiest)
sudo snap install powershell --classic

# Or via Microsoft apt repo — see: https://learn.microsoft.com/en-us/powershell/scripting/install/install-ubuntu
```

Verify:

```bash
pwsh --version
```

---

## Phase 4 — Editor

### VS Code

```bash
sudo snap install --classic code
```

Or via the official `.deb` package:

```bash
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor \
  | sudo tee /etc/apt/trusted.gpg.d/packages.microsoft.gpg > /dev/null
echo "deb [arch=amd64] https://packages.microsoft.com/repos/code stable main" \
  | sudo tee /etc/apt/sources.list.d/vscode.list
sudo apt update && sudo apt install -y code
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

## Phase 5 — Runtimes

### Node.js (via nvm)

See: [Node-260413a.md](Node-260413a.md)

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash
# Restart shell, then:
nvm install --lts
nvm use --lts
node -v && npm -v
```

### .NET SDK

```bash
# Add Microsoft package repo
wget https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb

sudo apt update && sudo apt install -y dotnet-sdk-8.0
```

Verify:

```bash
dotnet --version
dotnet --list-sdks
```

---

## Phase 6 — Cloud & DevOps

### Azure CLI

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
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

## Phase 7 — Containers

### Docker Engine

```bash
# Add Docker's official GPG key and repo
curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
  | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Allow running docker without sudo
sudo usermod -aG docker $USER
newgrp docker
```

Verify:

```bash
docker --version
docker run hello-world
```

---

## Phase 8 — AI Coding Assistants

### GitHub Copilot

Installed via VS Code extensions in Phase 4. Sign in through VS Code's Accounts menu.

### Claude Code CLI

Requires Node.js (Phase 5). See: [claude-cli-install-260413a.md](claude-cli-install-260413a.md)

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

[1] [GitHub CLI install – Linux](https://github.com/cli/cli/blob/trunk/docs/install_linux.md)  
[2] [.NET on Ubuntu – Microsoft](https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu)  
[3] [Azure CLI on Linux – Microsoft](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux)  
[4] [Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)  
[5] [VS Code on Linux](https://code.visualstudio.com/docs/setup/linux)
