# Install Gemini CLI

**Date:** 2026-04-11  
**Category:** environment  
**Tags:** `gemini`, `google`, `cli`, `install`, `npm`, `windows`  
**Related:** [claude-cli-install-260413a.md](claude-cli-install-260413a.md), [codex-cli-install-260411a.md](codex-cli-install-260411a.md)

---

## TL;DR

- Install via npm: `npm install -g @google/gemini-cli`
- Requires Node.js version 18 or higher
- First run prompts for Google Account authentication
- Can run instantly with npx: `npx @google/gemini-cli`

---

## 1. Install Prerequisites

* Node.js: Node.js (version 18 or higher) is required.
* To check if Node.js is installed, open PowerShell or Command Prompt and type: `node --version`
* If Node.js is not installed, download the Windows installer from the [Official Node.js Website](https://nodejs.org). [1, 4, 5, 6] 

---

## 2. Install Gemini CLI

After Node.js is installed, run the following command in your terminal to install the CLI globally: [4, 7] 

```powershell
npm install -g @google/gemini-cli
```

* Alternatively, run it instantly using npx: [7, 8] 

```powershell
npx @google/gemini-cli
```

---

## 3. Authenticate and Run

* Launch: Start the tool by typing `gemini` in your terminal.
* Authentication: The CLI will prompt you to log in on the first run.
* Follow the link provided to sign in with your Google Account.
* If you are using a Google Workspace account, you may need to set a `GOOGLE_CLOUD_PROJECT` environment variable. [2, 4, 6, 7, 10, 11] 

---

## Alternative: Windows Subsystem for Linux (WSL)

For a better development environment, some users prefer running the CLI through **WSL**: [12, 14, 15] 

1. Open PowerShell as Administrator and run `wsl --install`.
2. Restart your computer and set up your Linux (Ubuntu) username.
3. Install Node.js within the Linux terminal and then use the `npm` command above. [4, 12, 16] 

---

## Sources

[1] [https://www.youtube.com/watch?v=lMoOS2DZfKE](https://www.youtube.com/watch?v=lMoOS2DZfKE)
[2] [https://www.youtube.com/watch?v=v3QEdKkFdGM&t=17](https://www.youtube.com/watch?v=v3QEdKkFdGM&t=17)
[3] [https://geminicli.com/docs/get-started/installation/](https://geminicli.com/docs/get-started/installation/)
[4] [https://www.youtube.com/watch?v=we2HwLyKYEg](https://www.youtube.com/watch?v=we2HwLyKYEg)
[5] [https://www.reddit.com/r/GoogleGeminiAI/comments/1lkol0m/gemini_cli_a_comprehensive_guide_to_understanding/](https://www.reddit.com/r/GoogleGeminiAI/comments/1lkol0m/gemini_cli_a_comprehensive_guide_to_understanding/)
[6] [https://www.youtube.com/watch?v=ZXDcfOLP5zI](https://www.youtube.com/watch?v=ZXDcfOLP5zI)
[7] [https://geminicli.com/docs/get-started/installation/](https://geminicli.com/docs/get-started/installation/)
[8] [https://github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)
[9] [https://medium.com/@dorangao/comparing-codex-cli-vs-claude-code-vs-gemini-cli-ai-coding-tools-in-your-terminal-1a238c329cbe](https://medium.com/@dorangao/comparing-codex-cli-vs-claude-code-vs-gemini-cli-ai-coding-tools-in-your-terminal-1a238c329cbe)
[10] [https://geminicli.com/docs/get-started/authentication/](https://geminicli.com/docs/get-started/authentication/)
[11] [https://gemini-cli.org/posts/how-to-install-gemini-cli](https://gemini-cli.org/posts/how-to-install-gemini-cli)
[12] [https://www.linkedin.com/pulse/from-zero-hero-your-ultimate-guide-installing-gemini-cli-slobodian-4jbof](https://www.linkedin.com/pulse/from-zero-hero-your-ultimate-guide-installing-gemini-cli-slobodian-4jbof)
[13] [https://learn.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-windows](https://learn.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-windows)
[14] [https://www.analyticsvidhya.com/blog/2026/01/gemini-3-pro-cli/](https://www.analyticsvidhya.com/blog/2026/01/gemini-3-pro-cli/)
[15] [https://arstechnica.com/ai/2026/03/googles-new-command-line-tool-can-plug-openclaw-into-your-workspace-data/](https://arstechnica.com/ai/2026/03/googles-new-command-line-tool-can-plug-openclaw-into-your-workspace-data/)
[16] [https://inceptivetechnologies.com/google-gemini-cli-top-open-source-ai-tool-for-developers/](https://inceptivetechnologies.com/google-gemini-cli-top-open-source-ai-tool-for-developers/)
[17] [https://medium.com/@jmihir/explore-flutter-extensions-with-gemini-cli-an-in-depth-guide-for-developers-a9e8a290fd26](https://medium.com/@jmihir/explore-flutter-extensions-with-gemini-cli-an-in-depth-guide-for-developers-a9e8a290fd26)
[18] [https://docs.cloud.google.com/gemini/docs/codeassist/gemini-cli](https://docs.cloud.google.com/gemini/docs/codeassist/gemini-cli)
