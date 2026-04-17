# Codex CLI Install

**Date:** 2026-04-11  
**Category:** environment  
**Tags:** `codex`, `openai`, `cli`, `install`, `npm`, `windows`  
**Related:** [Install Claude Code CLI](claude-cli-install-260413a.md)

---

## TL;DR

- Install via npm: `npm install -g @openai/codex`
- Requires Node.js version 22 or later
- First run opens browser for ChatGPT authentication
- WSL recommended for best experience on Windows

---

## Prerequisites

* Node.js: Version 22 or later is required. If you don't have it, download the LTS version from Nodejs.org.
* A ChatGPT Account: You will need to sign in with your ChatGPT account (Plus, Pro, Business, Edu, or Enterprise) to use the CLI. [1, 2, 5, 6] 

---

## Installation Steps

1. Open your terminal: Open PowerShell or Windows Terminal as an Administrator.
2. Verify Node.js: Ensure Node and npm are correctly installed by running:
``` powershell
node -v
npm -v
```   
3. Install Codex CLI: Run the following command to install the package globally:
``` powershell   
npm install -g @openai/codex
```   
4. Launch & Authenticate: Type `codex` to start the interface.
   * The first time you run it, a browser window will open for you to [authenticate with your ChatGPT account](https://developers.openai.com/codex/quickstart).
   * Alternatively, you can provide an OpenAI API key if prompted. [1, 6, 7, 8, 9] 

---

## Alternative: Windows Subsystem for Linux (WSL)

For a more stable environment, OpenAI recommends installing via WSL: [9] 

1. Enable WSL: Run `wsl --install` in an elevated PowerShell and restart your PC.
2. Install in Linux: Once inside your Linux distribution (e.g., Ubuntu), follow the same npm installation command:
```bash
npm install -g @openai/codex
```
[9, 10, 11, 12, 13] 

---

## Quick Tips

* Updates: Keep your CLI up to date by running `npm i -g @openai/codex@latest`.
* App Version: If you prefer a GUI, a [Codex desktop app](https://developers.openai.com/codex/app/windows) is also available through the Microsoft Store. [1, 14] 

---

## Node.js

To install the OpenAI Codex CLI on Windows, install Node.js (LTS version), then run in Command Prompt or PowerShell. After installation, run to authenticate via browser, which requires a ChatGPT Plus/Team/Ent plan or API key. Experimental Windows support is best used via WSL2. 

### Prerequisites

* Node.js & npm: Required for package installation. Download from [nodejs.org](https://nodejs.org)
* OpenAI Account: A ChatGPT Plus, Team, or Enterprise plan is recommended for access. [2, 6, 7, 8, 9]  

### Step-by-Step Installation

1. Install Node.js: Download and run the Windows installer from [NodeJS](https://nodejs.org)
2. Open Terminal: Open Command Prompt or PowerShell as Administrator. 
3. Verify Node.js: Type to ensure it is installed. 
4. Install Codex CLI: Run the following command to install globally: 
5. Authenticate: Type in the terminal and follow the prompts to log in via your web browser. [1, 4, 5, 6, 7]  

This video shows the installation process for the Codex CLI on Windows: 
> [!NOTE]
> Watch this short video for more...
> [![Watch this Video](https://img.youtube.com/vi/2MFDSeRjHZE/hqdefault.jpg)](https://youtube.com/watch?v=2MFDSeRjHZE)

---

## Winget

### Alternative Installation (Winget)

If you have WinGet installed, you can use the following command: [10]  

```powershell
winget install OpenAI.Codex
```

---

## Usage

Once installed, you can use Codex within any directory by typing in your terminal to begin interacting with the AI agent. [1, 5, 7]  

Note: For the most stable experience on Windows, using Windows Subsystem for Linux (WSL2) is recommended by OpenAI. [3]  

---

## Sources

[1] [https://developers.openai.com/codex/cli](https://developers.openai.com/codex/cli)
[2] [https://www.deployhq.com/blog/getting-started-with-openai-codex-cli-ai-powered-code-generation-from-your-terminal](https://www.deployhq.com/blog/getting-started-with-openai-codex-cli-ai-powered-code-generation-from-your-terminal)
[3] [https://developers.openai.com/codex/windows](https://developers.openai.com/codex/windows)
[4] [https://www.npmjs.com/package/@openai/codex](https://www.npmjs.com/package/@openai/codex)
[5] [https://www.youtube.com/watch?v=2MFDSeRjHZE](https://www.youtube.com/watch?v=2MFDSeRjHZE)
[6] [https://github.com/openai/codex](https://github.com/openai/codex)
[7] [https://developers.openai.com/codex/quickstart](https://developers.openai.com/codex/quickstart)
[8] [https://www.linkedin.com/pulse/installing-openai-codex-cli-windows-11-carlos-miranda-levy-2o4ee](https://www.linkedin.com/pulse/installing-openai-codex-cli-windows-11-carlos-miranda-levy-2o4ee)
[9] [https://www.mostlyserious.io/insights/claude-code-codex-guide-nontechnical](https://www.mostlyserious.io/insights/claude-code-codex-guide-nontechnical)
[10] [https://winstall.app/apps/OpenAI.Codex](https://winstall.app/apps/OpenAI.Codex)
