# MCP Basics on Windows with C#

**Date:** 2026-05-01  
**Category:** engineering  
**Tags:** `mcp`, `windows`, `csharp`, `dotnet`, `copilot`  
**Related:** [Workstation Setup — Windows 10 / 11](../environment/workstation-setup-windows-260413a.md)

---

## TL;DR

- MCP is the standard way an AI host like VS Code or Visual Studio talks to external tools
- On Windows, the easiest first step is a local **stdio** MCP server built as a .NET console app
- For most C# projects, start with the `ModelContextProtocol` NuGet package
- Wire the server into `.vscode\mcp.json` or `%USERPROFILE%\.mcp.json` and let the host discover its tools
- For stdio servers, keep `stdout` clean; send logs to `stderr`

---

## What MCP is

**Model Context Protocol (MCP)** is an open standard for connecting AI applications to external systems such as files, databases, APIs, prompts, and tools. Think of it as the contract between an AI host and the things it can use. [1]

For a Windows + C# mental model, keep it simple:

- **Host / client** — VS Code, Visual Studio, Claude Desktop, or another AI app
- **MCP server** — your local or remote process that exposes capabilities
- **Tools / resources / prompts** — the things the host can discover and use through that server
- **Transport** — how they talk; for first steps on Windows, **stdio** is the easiest place to start

If you only want one sentence to remember: **the editor is the client, your C# app is the server, and MCP is the protocol between them**.

---

## Install the Windows prerequisites

If your workstation already has .NET and VS Code, skip this section.

```powershell
winget install --id Microsoft.DotNet.SDK.8 -e
winget install --id Microsoft.VisualStudioCode -e

code --install-extension ms-dotnettools.csharp
code --install-extension ms-dotnettools.csdevkit

dotnet --version
```

> [!TIP]
> If you want a fuller Windows setup baseline, see [Workstation Setup — Windows 10 / 11](../environment/workstation-setup-windows-260413a.md).

---

## Build a minimal C# MCP server

The official C# SDK recommends starting with the `ModelContextProtocol` package for stdio-based servers. [2]

Create a console app:

```powershell
New-Item -ItemType Directory -Path C:\work\mcp-echo -Force
Set-Location C:\work\mcp-echo

dotnet new console -n McpEcho
Set-Location C:\work\mcp-echo\McpEcho

dotnet add package ModelContextProtocol
dotnet add package Microsoft.Extensions.Hosting
```

Replace `Program.cs` with:

```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
using ModelContextProtocol.Server;
using System.ComponentModel;

var builder = Host.CreateApplicationBuilder(args);
builder.Logging.AddConsole(options =>
{
    // For stdio MCP servers, keep stdout reserved for protocol messages.
    options.LogToStandardErrorThreshold = LogLevel.Trace;
});

builder.Services
    .AddMcpServer()
    .WithStdioServerTransport()
    .WithToolsFromAssembly();

await builder.Build().RunAsync();

[McpServerToolType]
public static class EchoTools
{
    [McpServerTool, Description("Echo a short message back to the MCP client.")]
    public static string Echo(string message) => $"Echo from C#: {message}";
}
```

This gives you a working MCP server with one tool named `Echo`. The key pieces are:

- `AddMcpServer()` — registers MCP services
- `WithStdioServerTransport()` — uses local standard input/output transport
- `WithToolsFromAssembly()` — finds methods marked with `[McpServerTool]`

---

## Connect it to VS Code on Windows

VS Code can load MCP servers from a workspace file at `.vscode\mcp.json` or from your user profile configuration. [3]

Create `.vscode\mcp.json` in the folder where you want to use the tool:

```json
{
  "servers": {
    "echo-csharp": {
      "command": "dotnet",
      "args": [
        "run",
        "--project",
        "C:\\work\\mcp-echo\\McpEcho\\McpEcho.csproj"
      ]
    }
  }
}
```

Then:

1. Open the folder in VS Code.
2. Let VS Code trust and start the server.
3. Open Chat and enable the `echo-csharp` tools if prompted.
4. Ask for a tool-based action.

Example prompt:

```text
Use the echo-csharp tool and send the text: hello from Windows
```

> [!IMPORTANT]
> Use absolute Windows paths in `mcp.json`. That avoids ambiguity when VS Code starts the server from a different working directory.

---

## Use Visual Studio instead

Visual Studio also supports MCP on Windows. The most useful file locations are:

- `%USERPROFILE%\.mcp.json` for a global user-level configuration
- `<SOLUTIONDIR>\.mcp.json` for a repo or solution-level configuration [4]

The same `dotnet run --project ...` approach works well for a first local server. Visual Studio will discover the server, list its tools, and ask for approval before tool use.

---

## Know the first gotchas

### stdout vs stderr

For a **stdio** server, do not write diagnostic output to `stdout`. That stream is reserved for MCP protocol messages. Log to `stderr` instead. This is one of the fastest ways to avoid a mysteriously broken local server. [1, 2]

### Start with stdio, not HTTP

HTTP-based MCP servers are useful later, especially for shared services or remote auth flows, but they add more moving parts. A local stdio server is the fastest way to understand the protocol.

### Tool approvals are normal

Both VS Code and Visual Studio can ask you to trust the server and approve tool execution. That is expected behavior, not a failure. [3, 4]

### Windows sandboxing is not there in VS Code

VS Code documents sandboxing for local stdio MCP servers on macOS and Linux, but not on Windows. On Windows, trust the server source before enabling it. [3]

---

## Where to go next

Once the echo tool works, the next useful step is to replace it with a real tool:

- read a local file
- call a REST API
- query a small database
- wrap an internal script or PowerShell workflow

That is usually the moment MCP stops feeling abstract and starts feeling practical.

---

## Sources

[1] [Model Context Protocol Introduction](https://modelcontextprotocol.io/introduction)  
[2] [MCP C# SDK — Getting Started](https://csharp.sdk.modelcontextprotocol.io/concepts/getting-started.html)  
[3] [VS Code — Add and Manage MCP Servers](https://code.visualstudio.com/docs/copilot/chat/mcp-servers)  
[4] [Visual Studio — Use MCP Servers](https://learn.microsoft.com/en-us/visualstudio/ide/mcp-servers?view=visualstudio)
