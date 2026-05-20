# Windows Quick Install and Verification Cheat Sheet

This is a short Windows setup guide for Git, Node.js, Claude Code, and CC Switch. It keeps only the commands and checks most users need.

> Note: Claude Code currently supports native Windows PowerShell and CMD. Git for Windows is still recommended because Claude Code can use Git Bash internally for Unix-like command execution. WSL is useful when your project lives in a Linux toolchain. For the latest installer behavior, refer to the [official Claude Code Setup documentation](https://code.claude.com/docs/en/setup).

## Useful Websites

| Tool | Website | Purpose |
| --- | --- | --- |
| Git for Windows | [https://git-scm.com/download/win](https://git-scm.com/download/win) | Download Git and Git Bash |
| Node.js | [https://nodejs.org/](https://nodejs.org/) | Download Node.js LTS |
| Claude Code Docs | [https://code.claude.com/docs/](https://code.claude.com/docs/) | Read the official Claude Code documentation |
| Claude Code Setup | [https://code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup) | Check the latest Windows installation commands |
| Anthropic Console | [https://console.anthropic.com/](https://console.anthropic.com/) | Manage Anthropic API keys |
| CC Switch | [https://ccswitch.io/](https://ccswitch.io/) | Download CC Switch if you need model switching |

## Quick Install and Verification Guide

### Git

Option 1: download the official installer.

Open the Git for Windows website, download the `.exe` installer, and install it:

[https://git-scm.com/download/win](https://git-scm.com/download/win)

Option 2: install with WinGet.

```powershell
winget install --id Git.Git -e --source winget
```

Verify:

```powershell
git --version
```

Expected output looks like this:

```text
git version 2.54.0.windows.1
```

Notes:

- During installation, keep the Add to PATH option enabled.
- After installation, close and reopen PowerShell, CMD, or Git Bash before testing.
- The common Git Bash path is `C:\Program Files\Git\bin\bash.exe`.

### Node.js

Install:

1. Open the Node.js website: [https://nodejs.org/](https://nodejs.org/)
2. Download the LTS `.msi` installer.
3. Run the installer.
4. Keep the Add to PATH option enabled.

Verify:

```powershell
node -v
npm -v
```

### Claude Code

Recommended option 1: official Windows installer.

PowerShell:

```powershell
irm https://claude.ai/install.ps1 | iex
```

CMD:

```cmd
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

WinGet:

```powershell
winget install Anthropic.ClaudeCode
```

Optional option 2: npm installation.

If Node.js is already installed, you can also use npm. Refer to the official documentation for the latest npm support notes.

```bash
npm install -g @anthropic-ai/claude-code
```

Verify:

```powershell
claude --version
```

Or run a simple test:

```powershell
claude "Hello"
```

Start interactive mode:

```powershell
claude
```

Login inside Claude Code:

```text
/login
```

Notes:

- Claude Code can be installed and launched from native Windows PowerShell or CMD.
- If shell commands, paths, or Unix-like tools behave oddly, install Git for Windows and try Git Bash.
- If your project is Linux-based, use WSL and install Claude Code inside the WSL terminal.
- A stable network is required. API-based usage also requires a valid API key.
- Never share API keys, tokens, or private Base URLs. Do not commit them to GitHub.

## Troubleshooting Tips

### 1. Command Not Found After Installation

Most of the time, PATH has not refreshed yet.

Fix:

1. Close the current PowerShell, CMD, or Git Bash window.
2. Open a new terminal.
3. Run the checks again.

```powershell
git --version
node -v
npm -v
claude --version
```

### 2. Do Not Mix PowerShell and CMD Commands

PowerShell installer:

```powershell
irm https://claude.ai/install.ps1 | iex
```

CMD installer:

```cmd
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

If `irm` is not recognized, you are probably in CMD.

If `&&` reports a syntax error, you may be in PowerShell.

### 3. Claude Code Behaves Oddly in CMD

Claude Code supports native Windows, but shell, PATH, Git Bash, and permission settings can vary by machine.

Try this order:

1. Reopen CMD.
2. Test in PowerShell.
3. Install Git for Windows and test in Git Bash.
4. If the project uses a Linux toolchain, use WSL.

### 4. Minimal Health Check

```powershell
git --version
node -v
npm -v
claude --version
```

If all commands print version numbers, the basic development environment is ready.

## CC Switch Short Note

If you also need CC Switch to switch between DeepSeek, Qwen, GLM, Kimi, SiliconFlow, OpenRouter, or other providers, download it only from official sources:

- Website: [https://ccswitch.io/](https://ccswitch.io/)
- GitHub: [https://github.com/farion1231/cc-switch](https://github.com/farion1231/cc-switch)
- Releases: [https://github.com/farion1231/cc-switch/releases](https://github.com/farion1231/cc-switch/releases)

> Note: Do not download CC Switch from random cloud-drive links, private-message links, ad sites, or repackaged installers. Never expose API keys, tokens, or Base URLs.

If installation fails, send the terminal error output to technical support. Mask any API key before sharing screenshots.
