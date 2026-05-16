# Complete Guide: Setting Up Claude Code on Windows and Switching Models with CC Switch

> Note: This guide explains what to install and how to verify the setup. It does not run any installation command for you. When a setting, model name, Base URL, or installer changes, refer to the official documentation.

## Useful Websites

You only need accounts for the platforms you actually use. For example, if you only use DeepSeek, you do not need to register for Qwen, GLM, Kimi, or OpenRouter.

| Website | Purpose |
| --- | --- |
| [Claude Code Documentation](https://code.claude.com/docs/) | Main documentation for Claude Code installation, configuration, permissions, environment variables, and troubleshooting. |
| [Claude Code Quickstart](https://code.claude.com/docs/en/quickstart) | Basic `claude` command usage, login flow, project startup, and common commands. |
| [Claude Code Setup](https://code.claude.com/docs/en/setup) | Windows setup, PowerShell/CMD differences, Git Bash notes, and system requirements. |
| [Claude Code Environment Variables](https://code.claude.com/docs/en/env-vars) | Official reference for `ANTHROPIC_API_KEY`, `ANTHROPIC_BASE_URL`, `CLAUDE_CODE_GIT_BASH_PATH`, and related variables. |
| [Claude Code Settings](https://code.claude.com/docs/en/settings) | `settings.json`, `/config`, user settings, and project settings. |
| [Anthropic Console](https://console.anthropic.com/) | Create and manage Anthropic API keys. |
| [CC Switch Website](https://ccswitch.io/) | Learn about and download CC Switch. |
| [CC Switch GitHub](https://github.com/farion1231/cc-switch) | Source code, documentation, release notes, and security warnings. |
| [CC Switch Releases](https://github.com/farion1231/cc-switch/releases) | Download the Windows installer. |
| [Homebrew](https://brew.sh/) | macOS package manager; listed here for cross-platform reference. |
| [Git](https://git-scm.com/) | Git documentation and downloads. |
| [VS Code](https://code.visualstudio.com/) | Code editor and project workspace. |
| [Python](https://www.python.org/downloads/macos/) | Python downloads; use the Windows download page from python.org when installing on Windows. |
| [Node.js](https://nodejs.org/) | Node.js LTS downloads and documentation. |
| [DeepSeek Platform](https://platform.deepseek.com/) | DeepSeek API keys, billing, and account status. |
| [DeepSeek API Docs](https://api-docs.deepseek.com/) | DeepSeek Base URL, model names, and API formats. |
| [Alibaba Cloud Bailian / DashScope](https://bailian.console.aliyun.com/) | Qwen API keys, model access, and usage. |
| [DashScope Documentation](https://help.aliyun.com/zh/model-studio/) | Qwen models, OpenAI-compatible API, and calling formats. |
| [Zhipu AI](https://open.bigmodel.cn/) | GLM API keys and model access. |
| [Kimi / Moonshot](https://platform.moonshot.cn/) | Kimi API keys and model access. |
| [SiliconFlow](https://siliconflow.cn/) | API keys for Chinese and open-source models. |
| [OpenRouter](https://openrouter.ai/) | Multi-model routing API. |
| [New API](https://github.com/Calcium-Ion/new-api) | Self-hosted or managed OpenAI-compatible API gateway. |
| [One API](https://github.com/songquanpeng/one-api) | Self-hosted or managed OpenAI-compatible API gateway. |

> Note: Download CC Switch only from the official website or GitHub Releases. Do not use random cloud-drive links, private-message links, repackaged installers, or unknown download sites.

## 1. What Claude Code Is

Claude Code is an AI coding assistant that runs from your terminal. It can inspect a project, edit files, run commands, help debug issues, review changes, and assist with day-to-day software development.

## 2. What CC Switch Is

CC Switch is a configuration and model-switching tool. Instead of manually editing environment variables and API settings every time you switch providers, you can manage providers such as DeepSeek, Qwen, GLM, Kimi, SiliconFlow, or OpenRouter in one place.

## 3. What DeepSeek / Qwen / GLM / Kimi Are

DeepSeek, Qwen, GLM, and Kimi are different AI model providers. In this workflow:

| Component | Simple explanation |
| --- | --- |
| Claude Code | The AI coding workspace |
| DeepSeek / Qwen / GLM / Kimi | The AI brains you can switch between |
| CC Switch | The model switcher and configuration manager |

## 4. Required Tools

| Tool | Required | Purpose |
| --- | --- | --- |
| Windows 10/11 | Required | Operating system |
| PowerShell / Windows Terminal | Required | Run setup and verification commands |
| Git for Windows | Strongly recommended | Provides Git and Git Bash |
| Claude Code | Required | AI coding assistant |
| Claude account or API key | At least one | Login or model access |
| Stable network | Required | Downloads and API calls |

Recommended tools:

| Tool | Purpose |
| --- | --- |
| VS Code | Code editing and project management |
| Python 3.10+ | Scripts, automation, and testing tools |
| Node.js LTS | Required by some CLI and frontend tools |
| GitHub account | Backup and version control |
| Windows Terminal | Better terminal experience |

## 5. Recommended Folder Structure

Use a simple English path:

```text
C:\AI-Tools
├── ClaudeCode
├── CC-Switch
├── Projects
├── Docs
└── Backup
```

Recommendations:

| Recommendation | Why |
| --- | --- |
| Avoid the Desktop | Desktop folders may be synced by OneDrive and can cause permission confusion. |
| Avoid non-English paths | Some CLI tools still fail on non-ASCII paths. |
| Avoid special characters | Spaces, brackets, `#`, and `&` can break scripts. |
| Use short English paths | Easier to copy, debug, and document. |

## 6. PowerShell / CMD / Git Bash Differences

| Terminal | Prompt example | Best for |
| --- | --- | --- |
| PowerShell | `PS C:\Users\name>` | `irm`, `$env`, `setx` |
| CMD | `C:\Users\name>` | `curl`, `&&`, `set` |
| Git Bash | `user@PC MINGW64 ~` | `ls`, `bash`, Unix-like commands |

> Note: `irm` is a PowerShell command. It will not work in CMD.

> Note: `&&` is common in CMD and Git Bash. If a command fails in PowerShell, first confirm which terminal you are using.

## 7. Install Git for Windows

Download:

[https://git-scm.com/download/win](https://git-scm.com/download/win)

After installation, reopen your terminal and verify:

```powershell
git --version
```

The default Git Bash path is commonly:

```text
C:\Program Files\Git\bin\bash.exe
```

Verify Git Bash:

```powershell
"C:\Program Files\Git\bin\bash.exe" --version
```

If Claude Code cannot find Git Bash, you may set `CLAUDE_CODE_GIT_BASH_PATH` in Claude Code settings. The exact location and supported fields should follow the official Claude Code Settings documentation.

Example JSON:

```json
{
  "env": {
    "CLAUDE_CODE_GIT_BASH_PATH": "C:\\Program Files\\Git\\bin\\bash.exe"
  }
}
```

## 8. Install Claude Code

Always check the official setup page first:

[https://code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup)

Choose one installation method.

### Option 1: PowerShell

Run in PowerShell:

```powershell
irm https://claude.ai/install.ps1 | iex
```

### Option 2: CMD

Run in CMD:

```cmd
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

### Option 3: WinGet

Run in PowerShell or CMD:

```powershell
winget install Anthropic.ClaudeCode
```

Verify:

```powershell
claude --version
```

Start Claude Code:

```powershell
claude
```

If supported by your installed version:

```powershell
claude doctor
```

Login inside Claude Code:

```text
/login
```

Common commands:

```text
/help
/login
/model
/resume
```

> Note: If Windows says `claude` is not recognized, the PATH may not be refreshed. Close and reopen the terminal. If it still fails, restart Windows or reinstall using the official instructions.

## 9. Environment Variables

Only configure API environment variables when you use API-based access, CC Switch, a third-party provider, or a compatible gateway. If you only use official Claude login, keep the setup simple first.

### PowerShell temporary variables

```powershell
$env:ANTHROPIC_API_KEY="YOUR_API_KEY"
$env:ANTHROPIC_BASE_URL="YOUR_BASE_URL"
```

View them:

```powershell
echo $env:ANTHROPIC_API_KEY
echo $env:ANTHROPIC_BASE_URL
```

### CMD temporary variables

```cmd
set ANTHROPIC_API_KEY=YOUR_API_KEY
set ANTHROPIC_BASE_URL=YOUR_BASE_URL
```

View them:

```cmd
echo %ANTHROPIC_API_KEY%
echo %ANTHROPIC_BASE_URL%
```

### Git Bash temporary variables

```bash
export ANTHROPIC_API_KEY="YOUR_API_KEY"
export ANTHROPIC_BASE_URL="YOUR_BASE_URL"
```

View them:

```bash
echo $ANTHROPIC_API_KEY
echo $ANTHROPIC_BASE_URL
```

### Permanent user variables

Run in PowerShell or CMD:

```powershell
setx ANTHROPIC_API_KEY "YOUR_API_KEY"
setx ANTHROPIC_BASE_URL "YOUR_BASE_URL"
```

Reopen the terminal after `setx`.

Important variables:

| Variable | Meaning |
| --- | --- |
| `ANTHROPIC_API_KEY` | API key |
| `ANTHROPIC_BASE_URL` | Custom API endpoint |
| `ANTHROPIC_AUTH_TOKEN` | Custom bearer token, refer to the official documentation |
| `ANTHROPIC_CUSTOM_HEADERS` | Custom headers, refer to the official documentation |
| `ANTHROPIC_CUSTOM_MODEL_OPTION` | Custom model option, refer to the official documentation |
| `ENABLE_TOOL_SEARCH` | May be needed for some non-official Base URLs, refer to the provider and tool documentation |
| `CLAUDE_CODE_GIT_BASH_PATH` | Path to Git Bash on Windows |

> Note: Never commit API keys to GitHub, paste them into public chats, or share screenshots that reveal them. If a key leaks, revoke it immediately on the provider platform.

## 10. Install CC Switch

Official sources:

- [CC Switch Website](https://ccswitch.io/)
- [CC Switch GitHub](https://github.com/farion1231/cc-switch)
- [CC Switch Releases](https://github.com/farion1231/cc-switch/releases)

Recommended process:

1. Open the official website or GitHub Releases page.
2. Download the Windows installer, commonly named like `CC-Switch-v{version}-Windows.msi`.
3. Install it normally.
4. Open CC Switch.

> Note: Be careful with fake CC Switch pages. Any page asking for payment, recharge, provider login credentials, or unusual permissions should be treated as suspicious.

## 11. Adding Providers in CC Switch

Typical provider fields:

| Field | Meaning |
| --- | --- |
| Provider Name | A friendly name, such as DeepSeek |
| API Key | The provider API key |
| Base URL | The provider API endpoint |
| Model Name | The model to use |
| Target App | Usually Claude Code |
| Apply / Switch | Enable the selected provider |

Workflow:

1. Open CC Switch.
2. Add a new Provider.
3. Choose a preset or enter settings manually.
4. Paste the API Key.
5. Enter the Base URL.
6. Enter the Model Name.
7. Select Claude Code as the target app.
8. Click Apply / Switch.
9. Restart Claude Code.
10. Test a short prompt.

## 12. DeepSeek Example

Platform:

[https://platform.deepseek.com/](https://platform.deepseek.com/)

API docs:

[https://api-docs.deepseek.com/](https://api-docs.deepseek.com/)

Example:

```text
Provider Name: DeepSeek
API Key: YOUR_API_KEY
Base URL: refer to the DeepSeek official documentation
Model Name: refer to the DeepSeek official documentation
Target App: Claude Code
```

If a provider supports an Anthropic-compatible endpoint, the Base URL may differ from the OpenAI-compatible endpoint. Refer to the official documentation.

## 13. Qwen Example

Console:

[https://bailian.console.aliyun.com/](https://bailian.console.aliyun.com/)

Documentation:

[https://help.aliyun.com/zh/model-studio/](https://help.aliyun.com/zh/model-studio/)

Example:

```text
Provider Name: Qwen
API Key: YOUR_API_KEY
Base URL: refer to the DashScope official documentation
Model Name: qwen-plus / qwen-max / qwen-coder or another official model name
Target App: Claude Code
```

> Note: DashScope may have different regions, endpoints, and calling formats. Refer to the official documentation.

## 14. GLM / Kimi / SiliconFlow / OpenRouter Examples

| Provider | Website | What to check |
| --- | --- | --- |
| GLM | [https://open.bigmodel.cn/](https://open.bigmodel.cn/) | API key, Base URL, model name, account permissions |
| Kimi | [https://platform.moonshot.cn/](https://platform.moonshot.cn/) | API key, Base URL, model name, account permissions |
| SiliconFlow | [https://siliconflow.cn/](https://siliconflow.cn/) | API key, Base URL, model name, model availability |
| OpenRouter | [https://openrouter.ai/](https://openrouter.ai/) | API key, Base URL, model route, pricing, rate limits |

General workflow:

1. Register or sign in to the provider.
2. Create an API key.
3. Read the official Base URL.
4. Read the current model name.
5. Add the provider in CC Switch.
6. Apply / Switch.
7. Restart Claude Code.
8. Test with a short prompt.

## 15. Environment Verification Checklist

### Verify Git

```powershell
git --version
```

Expected: a Git version is displayed.

### Verify Git Bash

```powershell
"C:\Program Files\Git\bin\bash.exe" --version
```

Expected: GNU Bash version information is displayed.

### Verify Claude Code

```powershell
claude --version
```

Expected: Claude Code version is displayed.

### Verify Claude Code starts

```powershell
claude
```

Expected: Claude Code opens in the terminal.

### Verify login

Inside Claude Code:

```text
/login
```

Expected: login completes or the session is already logged in.

### Verify project read/write

PowerShell or CMD:

```cmd
mkdir C:\AI-Tools\Projects\demo
cd C:\AI-Tools\Projects\demo
claude
```

Inside Claude Code:

```text
Create test.md with the content "Claude Code Windows environment test succeeded".
```

After exiting:

```cmd
dir
```

Expected: `test.md` appears.

### Verify model switching

After switching providers in CC Switch:

1. Close Claude Code.
2. Reopen the terminal.
3. Enter the project directory.
4. Run `claude`.
5. Ask:

```text
Please confirm in one sentence that the current model endpoint is responding.
```

Expected: the model replies without API Key, Base URL, or `model not found` errors.

## 16. Troubleshooting FAQ

| Issue | Likely cause | Fix |
| --- | --- | --- |
| `claude` is not recognized | PATH not refreshed or installation failed | Reopen the terminal, restart Windows, or reinstall using official instructions. |
| `irm` is not recognized | PowerShell command used in CMD | Run it in PowerShell. |
| `&&` fails | CMD command used in PowerShell | Use CMD or split the command into separate commands. |
| Git Bash is missing | Git for Windows is not installed or installed elsewhere | Install Git for Windows and configure `CLAUDE_CODE_GIT_BASH_PATH` if needed. |
| API Key error | Key is wrong, expired, or copied with extra spaces | Regenerate the key and update CC Switch. |
| Base URL error | Endpoint is wrong or path is incorrect | Copy the endpoint from the provider's official docs. |
| `model not found` | Model name is outdated or unavailable | Check the provider's current model list. |
| Switching has no effect | Provider was not applied or Claude Code was not restarted | Apply / Switch, then restart Claude Code. |
| Chat works but coding tools fail | Provider may not fully support tool calling | Try a coding model, a compatible endpoint, or official Claude for comparison. |
| Many permission prompts | Claude Code is protecting file and command access | Read each prompt carefully and only allow commands you understand. |
| Chinese or space-containing path fails | Path parsing or encoding issue | Move the project to `C:\AI-Tools\Projects\demo`. |
| `setx` does not take effect | Current terminal still has old environment | Reopen the terminal. |
| CC Switch came from a suspicious site | Fake or repackaged installer | Delete it and download only from `ccswitch.io` or GitHub Releases. |
| Model is slow or fails | Network, rate limit, balance, or provider outage | Check balance, rate limits, network, and provider status. |

## 17. Minimal Setup Workflow

1. Install Git for Windows.
2. Install Claude Code.
3. Run `claude --version`.
4. Create a project folder.
5. Run `claude`.
6. Login to Claude Code.
7. Install CC Switch.
8. Add a DeepSeek / Qwen / GLM / Kimi provider.
9. Apply / Switch.
10. Restart Claude Code.
11. Test file read/write.
12. Test command execution.
13. Test model response.
