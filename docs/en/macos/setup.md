# Complete Guide: Setting Up Claude Code on macOS and Switching Models with CC Switch

> Note: This guide explains how to set up a macOS environment for Claude Code, CC Switch, and third-party model providers. It does not run any installation command for you. When installer behavior, model names, Base URLs, or settings fields change, refer to the official documentation.

## Useful Websites

You only need accounts for the model platforms you actually plan to use.

| Website | Purpose |
| --- | --- |
| [Claude Code Documentation](https://code.claude.com/docs/) | Main documentation for Claude Code setup, usage, permissions, configuration, and troubleshooting. |
| [Claude Code Quickstart](https://code.claude.com/docs/en/quickstart) | First-run workflow, `claude` command usage, login, and common commands. |
| [Claude Code Setup](https://code.claude.com/docs/en/setup) | macOS installation methods, system requirements, verification, and update notes. |
| [Claude Code Environment Variables](https://code.claude.com/docs/en/env-vars) | Official reference for `ANTHROPIC_API_KEY`, `ANTHROPIC_BASE_URL`, and related variables. |
| [Claude Code Settings](https://code.claude.com/docs/en/settings) | `settings.json`, `/config`, user settings, and project settings. |
| [Anthropic Console](https://console.anthropic.com/) | Create and manage Anthropic API keys. |
| [CC Switch Website](https://ccswitch.io/) | Learn about and download CC Switch. |
| [CC Switch GitHub](https://github.com/farion1231/cc-switch) | Source code, documentation, release notes, and security warnings. |
| [CC Switch Releases](https://github.com/farion1231/cc-switch/releases) | Manually download macOS builds. |
| [Homebrew](https://brew.sh/) | Install and manage macOS development tools. |
| [Git](https://git-scm.com/) | Git downloads and documentation. |
| [VS Code](https://code.visualstudio.com/) | Code editor and project workspace. |
| [Python for macOS](https://www.python.org/downloads/macos/) | Python macOS downloads and documentation. |
| [Node.js](https://nodejs.org/) | Node.js LTS downloads and documentation. |
| [DeepSeek Platform](https://platform.deepseek.com/) | DeepSeek API keys, billing, and account status. |
| [DeepSeek API Docs](https://api-docs.deepseek.com/) | DeepSeek Base URL, model names, and API formats. |
| [Alibaba Cloud Bailian / DashScope](https://bailian.console.aliyun.com/) | Qwen API keys, model access, and usage. |
| [DashScope Documentation](https://help.aliyun.com/zh/model-studio/) | Qwen OpenAI-compatible API, model names, and calling formats. |
| [Zhipu AI](https://open.bigmodel.cn/) | GLM API keys and model access. |
| [Kimi / Moonshot](https://platform.moonshot.cn/) | Kimi API keys and model access. |
| [SiliconFlow](https://siliconflow.cn/) | API keys for Chinese and open-source models. |
| [OpenRouter](https://openrouter.ai/) | Multi-model routing API. |
| [New API](https://github.com/Calcium-Ion/new-api) | Self-hosted or managed OpenAI-compatible API gateway. |
| [One API](https://github.com/songquanpeng/one-api) | Self-hosted or managed OpenAI-compatible API gateway. |

> Note: Download CC Switch only from the official website or GitHub Releases. Do not use random cloud-drive links, private-message links, repackaged installers, or unknown download sites.

## 1. Who This Guide Is For

This guide is for macOS users who want to:

- Install Claude Code.
- Use CC Switch to manage model providers.
- Switch between DeepSeek, Qwen, GLM, Kimi, SiliconFlow, OpenRouter, or other compatible providers.
- Build a practical AI coding workflow on macOS.

In simple terms:

| Component | Meaning |
| --- | --- |
| Claude Code | The AI coding workspace that reads projects, edits files, and runs commands |
| DeepSeek / Qwen / GLM / Kimi | The AI models or model providers |
| CC Switch | The model switcher and configuration manager |
| API Key | The secret used to call a model API |
| Base URL | The model API endpoint |
| Model Name | The exact model you want to use |

## 2. Required and Recommended Tools

| Tool | Required | Purpose |
| --- | --- | --- |
| macOS | Required | Operating system |
| Terminal / iTerm2 | Required | Run setup and verification commands |
| Homebrew | Strongly recommended | Install Git, Node.js, Python, Claude Code, and CC Switch |
| Git | Strongly recommended | Project version control |
| Claude Code | Required | AI coding assistant |
| CC Switch | Optional but recommended | Manage and switch model providers |
| VS Code | Recommended | Edit code and documentation |
| Python 3.10+ | Recommended | Scripts, automation, and testing tools |
| Node.js LTS | Recommended | Required by some CLI and frontend tools |
| API Key | Required for third-party providers | Access model APIs |

## 3. Recommended Folder Structure

Use a simple English path:

```text
~/AI-Tools/
├── ClaudeCode/
├── CC-Switch/
├── Projects/
├── Docs/
└── Backup/
```

Recommendations:

| Recommendation | Why |
| --- | --- |
| Avoid the Desktop | Desktop folders may be synced by iCloud and can cause permission confusion. |
| Avoid non-English paths | Some CLI tools still fail on non-ASCII paths. |
| Avoid special characters | Spaces, brackets, `#`, and `&` can break scripts. |
| Use short English paths | Easier to copy, debug, and document. |

## 4. Install Homebrew

Website:

[https://brew.sh/](https://brew.sh/)

Install command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Verify:

```bash
brew --version
```

Apple Silicon Macs may need Homebrew added to the shell environment:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Common Homebrew paths:

| Mac type | Common path |
| --- | --- |
| Apple Silicon | `/opt/homebrew/bin/brew` |
| Intel | `/usr/local/bin/brew` |

## 5. Install Git

```bash
brew install git
```

Verify:

```bash
git --version
```

## 6. Install Node.js

```bash
brew install node
```

Verify:

```bash
node --version
npm --version
```

Node.js may not be required by every Claude Code installation path, but it is useful for general development and many CLI tools.

## 7. Install Python

```bash
brew install python
```

Verify:

```bash
python3 --version
pip3 --version
```

## 8. Install Claude Code

Always check the official Setup documentation first:

[https://code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup)

Common macOS options include the native installer and Homebrew. Use one installation method, not both unless you know why.

### Option 1: Native Installer

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Native installations may support automatic updates. Refer to the official documentation.

### Option 2: Homebrew

```bash
brew install --cask claude-code
```

Homebrew installations do not always auto-update. To update later, use the cask you installed and refer to the official documentation.

Verify:

```bash
claude --version
```

Start Claude Code:

```bash
claude
```

If supported by your installed version:

```bash
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

> Note: Claude Code access requirements can change. Account type, login flow, and API-based access should be checked against the official Claude Code documentation.

## 9. Install CC Switch

### Option 1: Homebrew

```bash
brew tap farion1231/ccswitch
brew install --cask cc-switch
```

Update later:

```bash
brew upgrade --cask cc-switch
```

### Option 2: Manual Download from GitHub Releases

Visit:

[https://github.com/farion1231/cc-switch/releases](https://github.com/farion1231/cc-switch/releases)

Download a macOS build such as:

```text
CC-Switch-v{version}-macOS.dmg
```

or:

```text
CC-Switch-v{version}-macOS.zip
```

Notes:

- Prefer the official website or GitHub Releases.
- Do not download from unknown cloud drives or private links.
- macOS may block apps from unidentified developers.
- If the app is blocked, confirm the source first, then allow it in System Settings > Privacy & Security.

## 10. Configure Environment Variables

The default shell on modern macOS is usually `zsh`.

Common shell files:

```text
~/.zshrc
~/.zprofile
```

Temporary variables for the current terminal:

```bash
export ANTHROPIC_API_KEY="YOUR_API_KEY"
export ANTHROPIC_BASE_URL="YOUR_BASE_URL"
```

Persist them for future terminal sessions:

```bash
echo 'export ANTHROPIC_API_KEY="YOUR_API_KEY"' >> ~/.zshrc
echo 'export ANTHROPIC_BASE_URL="YOUR_BASE_URL"' >> ~/.zshrc
source ~/.zshrc
```

View current values:

```bash
echo $ANTHROPIC_API_KEY
echo $ANTHROPIC_BASE_URL
```

Common variables:

| Variable | Meaning |
| --- | --- |
| `ANTHROPIC_API_KEY` | API key |
| `ANTHROPIC_BASE_URL` | Custom model endpoint |
| `ANTHROPIC_AUTH_TOKEN` | Bearer token, refer to the official documentation |
| `ANTHROPIC_CUSTOM_HEADERS` | Custom request headers, refer to the official documentation |

> Note: Do not share API keys, paste them into public tickets, commit them to GitHub, or send screenshots that reveal them. If a key leaks, revoke it immediately on the provider platform.

## 11. Configure Providers in CC Switch

Typical provider fields:

| Field | Meaning |
| --- | --- |
| Provider Name | Friendly name, such as DeepSeek |
| API Key | Provider API key |
| Base URL | Provider API endpoint |
| Model Name | Exact model name |
| Target App | Usually Claude Code |
| Apply / Switch | Enable the selected provider |

Workflow:

1. Open CC Switch.
2. Create a new Provider.
3. Enter the API Key.
4. Enter the Base URL.
5. Enter the Model Name.
6. Select Claude Code as the target app.
7. Click Apply / Switch.
8. Restart Claude Code.
9. Test a short prompt.

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

> Note: DeepSeek model names and endpoints may change. Always refer to the official DeepSeek documentation.

## 13. Qwen / GLM / Kimi / SiliconFlow / OpenRouter Examples

| Provider | Website | What to check |
| --- | --- | --- |
| Qwen / DashScope | [Alibaba Cloud Bailian](https://bailian.console.aliyun.com/) | API key, Base URL, model name, region, compatible API format |
| GLM | [Zhipu AI](https://open.bigmodel.cn/) | API key, Base URL, model name, account permissions |
| Kimi | [Moonshot](https://platform.moonshot.cn/) | API key, Base URL, model name, account permissions |
| SiliconFlow | [SiliconFlow](https://siliconflow.cn/) | API key, Base URL, model availability |
| OpenRouter | [OpenRouter](https://openrouter.ai/) | API key, Base URL, model route, pricing, rate limits |

General workflow:

1. Register or sign in to the provider.
2. Create an API key.
3. Read the official Base URL.
4. Read the current Model Name.
5. Add the provider in CC Switch.
6. Apply / Switch.
7. Restart Claude Code.
8. Test a short prompt.

> Note: OpenAI-compatible and Anthropic-compatible endpoints may be different. Refer to the official documentation for each provider.

## 14. Verify the Environment

### Homebrew

```bash
brew --version
```

### Git

```bash
git --version
```

### Node.js

```bash
node --version
npm --version
```

### Python

```bash
python3 --version
pip3 --version
```

### Claude Code

```bash
claude --version
claude
```

### Environment Variables

```bash
echo $ANTHROPIC_API_KEY
echo $ANTHROPIC_BASE_URL
```

### Project Read/Write Test

```bash
mkdir -p ~/AI-Tools/Projects/demo
cd ~/AI-Tools/Projects/demo
claude
```

Inside Claude Code:

```text
Create test.md with the content "Claude Code macOS environment test succeeded".
```

After exiting:

```bash
ls
```

Expected: `test.md` appears in the directory.

## 15. Troubleshooting FAQ

| Issue | Likely cause | Fix |
| --- | --- | --- |
| `brew: command not found` | Homebrew is not installed or PATH is not set | Install Homebrew from the official site and fix PATH. |
| `claude: command not found` | Claude Code is not installed or terminal PATH is stale | Reopen Terminal and check the official setup steps. |
| `.zshrc` changes do not apply | The file was not sourced or the wrong shell file was edited | Run `source ~/.zshrc` and open a new Terminal. |
| API Key error | Key is wrong, expired, or copied with spaces | Generate a new key and update CC Switch. |
| Base URL error | Endpoint or path is wrong | Copy the endpoint from the provider's official docs. |
| `model not found` | Model name is outdated or unavailable | Check the current provider model list. |
| CC Switch has no effect | Provider was not applied or Claude Code was not restarted | Apply / Switch, then restart Claude Code. |
| macOS blocks the app | Gatekeeper security check | Confirm the download source, then allow it in Privacy & Security. |
| Permission denied | Folder permissions or macOS privacy settings | Use `~/AI-Tools/Projects/` and check file permissions. |
| Non-English or space-containing paths fail | Path parsing or encoding issue | Move the project to a simple English path. |
| Chat works but tools fail | Provider may not fully support Claude Code tool calling | Try a coding model, compatible endpoint, or official Claude for comparison. |
| Network connection fails | Network, proxy, or provider outage | Check network, proxy, account status, and provider status. |

## 16. Minimal Setup Workflow

1. Install Homebrew.
2. Install Git.
3. Install Node.js and Python.
4. Install Claude Code using the official macOS instructions.
5. Run `claude --version`.
6. Create `~/AI-Tools/Projects/demo`.
7. Run `claude` and log in.
8. Install CC Switch.
9. Add a DeepSeek / Qwen / GLM / Kimi provider.
10. Apply / Switch, restart Claude Code, and test file access plus model response.
