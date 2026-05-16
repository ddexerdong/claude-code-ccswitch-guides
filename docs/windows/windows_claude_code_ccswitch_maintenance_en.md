# Maintenance Guide: Claude Code + CC Switch + Third-Party Models on Windows

> Note: This document is for ongoing maintenance and customer self-checks. It does not run any install, update, delete, or reset commands. For changing official tools, endpoints, model names, or settings fields, refer to the official documentation.

## Useful Maintenance Websites

| Website | Purpose |
| --- | --- |
| [Claude Code Documentation](https://code.claude.com/docs/) | Installation, configuration, permissions, environment variables, updates, and troubleshooting. |
| [Claude Code Quickstart](https://code.claude.com/docs/en/quickstart) | Basic startup, login, and common commands. |
| [Claude Code Setup](https://code.claude.com/docs/en/setup) | Windows setup, Git Bash, PowerShell/CMD notes, and system requirements. |
| [Claude Code Environment Variables](https://code.claude.com/docs/en/env-vars) | `ANTHROPIC_API_KEY`, `ANTHROPIC_BASE_URL`, `CLAUDE_CODE_GIT_BASH_PATH`, and related variables. |
| [Claude Code Settings](https://code.claude.com/docs/en/settings) | `settings.json`, `/config`, user settings, and project settings. |
| [Anthropic Console](https://console.anthropic.com/) | Anthropic API key management. |
| [CC Switch Website](https://ccswitch.io/) | Official CC Switch download and product information. |
| [CC Switch GitHub](https://github.com/farion1231/cc-switch) | Source code, documentation, updates, and security notes. |
| [CC Switch Releases](https://github.com/farion1231/cc-switch/releases) | Download the latest installer and view release notes. |
| [Homebrew](https://brew.sh/) | macOS package manager; included for cross-platform reference. |
| [Git](https://git-scm.com/) | Git documentation and downloads. |
| [VS Code](https://code.visualstudio.com/) | Code editor and project workspace. |
| [Python](https://www.python.org/downloads/macos/) | Python documentation and downloads; use the Windows page from python.org on Windows. |
| [Node.js](https://nodejs.org/) | Node.js LTS downloads and documentation. |
| [DeepSeek Platform](https://platform.deepseek.com/) | API keys, billing, model access, and status. |
| [DeepSeek API Docs](https://api-docs.deepseek.com/) | Base URL, model names, and API format. |
| [Alibaba Cloud Bailian / DashScope](https://bailian.console.aliyun.com/) | Qwen API keys, model access, and usage. |
| [DashScope Documentation](https://help.aliyun.com/zh/model-studio/) | OpenAI-compatible API, model names, and calling format. |
| [Zhipu AI](https://open.bigmodel.cn/) | GLM API keys and model access. |
| [Kimi / Moonshot](https://platform.moonshot.cn/) | Kimi API keys and model access. |
| [SiliconFlow](https://siliconflow.cn/) | API keys for Chinese and open-source models. |
| [OpenRouter](https://openrouter.ai/) | Multi-model routing API. |
| [New API](https://github.com/Calcium-Ion/new-api) | Self-hosted or managed OpenAI-compatible gateway. |
| [One API](https://github.com/songquanpeng/one-api) | Self-hosted or managed OpenAI-compatible gateway. |

> Note: Download CC Switch only from the official website or GitHub Releases. Do not use random cloud-drive links, private-message links, unknown download sites, or untrusted relay services.

## 1. What This Environment Includes

This maintenance guide assumes the Windows setup is already working:

| Component | Plain-English meaning | What to maintain |
| --- | --- | --- |
| Claude Code | AI coding workspace | Startup, login, file access, command execution |
| Git for Windows / Git Bash | Git and Bash command environment | `git` availability and Git Bash path |
| CC Switch | Provider configuration and model switcher | Current provider, API key, Base URL, model name |
| API Key | The password used to call a model API | Validity, rotation, leakage prevention |
| Base URL | The model API endpoint | Correct endpoint and path |
| Model Name | The exact model to use | Current availability and permissions |
| Environment variables | System-level configuration values | Old values, conflicts, and sensitive data |
| Project folder | Claude Code working directory | Read/write access and clean paths |

## 2. Quick Health Check Before Use

### PowerShell

```powershell
git --version
claude --version
echo $env:ANTHROPIC_API_KEY
echo $env:ANTHROPIC_BASE_URL
```

### CMD

```cmd
git --version
claude --version
echo %ANTHROPIC_API_KEY%
echo %ANTHROPIC_BASE_URL%
```

### Git Bash

```bash
git --version
claude --version
echo $ANTHROPIC_API_KEY
echo $ANTHROPIC_BASE_URL
```

Expected results:

| Check | Expected result |
| --- | --- |
| Git | Shows a Git version |
| Claude Code | Shows a Claude Code version |
| API Key | Present when using API-based providers; may be empty for official login |
| Base URL | Present when using third-party providers; may be empty for official login |

> Note: These commands may print sensitive API keys. Do not screenshot or forward the output unless the key is fully redacted.

## 3. Checking Claude Code

Run:

```powershell
claude --version
claude
```

Inside Claude Code, test file access:

```text
Create test.md with the content "Claude Code Windows environment test succeeded".
```

After exiting, check the folder:

```powershell
dir
```

Healthy behavior:

- Claude Code starts.
- `test.md` is created.
- Claude Code can read and write project files.
- Claude Code can run a simple command such as `dir`.

Common issues:

| Issue | What to do |
| --- | --- |
| `claude` is not recognized | Reopen the terminal, check PATH, and confirm installation. |
| Cannot start Claude Code | Check network, terminal, account, and official troubleshooting docs. |
| Cannot log in | Use `/login`, check browser redirect and account permissions. |
| Cannot read/write files | Move the project to a simple path such as `C:\AI-Tools\Projects\demo`. |
| Many permission prompts | Read each permission prompt carefully and approve only safe operations. |

## 4. Checking Git / Git Bash

Check Git:

```powershell
git --version
```

Check Git Bash:

```powershell
"C:\Program Files\Git\bin\bash.exe" --version
```

Notes:

| Item | Details |
| --- | --- |
| Git for Windows | Recommended for native Windows Claude Code usage |
| Common Git Bash path | `C:\Program Files\Git\bin\bash.exe` |
| Missing Git Bash | Set `CLAUDE_CODE_GIT_BASH_PATH` if needed |

Example settings JSON:

```json
{
  "env": {
    "CLAUDE_CODE_GIT_BASH_PATH": "C:\\Program Files\\Git\\bin\\bash.exe"
  }
}
```

> Note: The exact settings location and supported fields should follow the official Claude Code Settings documentation.

## 5. Checking CC Switch

Check:

| Item | What to verify |
| --- | --- |
| App opens | CC Switch window appears normally |
| Provider list | Your configured providers are visible |
| Current provider | The intended provider is selected |
| API Key | Present, valid, and from the correct platform |
| Base URL | Matches the provider's official docs |
| Model Name | Still available on the provider |
| Apply / Switch | The provider was actually applied |
| Claude Code restart | Claude Code was closed and reopened after switching |

Validation workflow:

1. Open CC Switch.
2. Switch to DeepSeek / Qwen / GLM / Kimi or another provider.
3. Click Apply / Switch.
4. Close the current Claude Code session.
5. Reopen PowerShell, CMD, or Git Bash.
6. Go to your project folder.
7. Run:

```powershell
claude
```

8. Ask:

```text
Please confirm in one sentence that the current model endpoint is responding.
```

Expected: a normal reply with no API Key error, Base URL error, `model not found`, 401, 403, 404, or 429.

## 6. Maintaining API Keys

Replace an API key when:

- The key was exposed.
- The key expired.
- The provider account changed.
- The customer changed accounts.
- The account has billing or permission issues.
- You see 401 Unauthorized.
- You see `invalid api key`.

Replacement workflow:

1. Sign in to the provider's official platform.
2. Revoke or disable the old key.
3. Create a new key.
4. Open CC Switch.
5. Replace the API Key.
6. Apply / Switch.
7. Restart Claude Code.
8. Test a short model response.

> Note: Never send API keys in chat, tickets, screenshots, README files, GitHub repositories, or shared documents. If a key may have leaked, revoke it immediately.

## 7. Maintaining Base URLs and Model Names

| Item | Meaning | Maintenance rule |
| --- | --- | --- |
| Base URL | API endpoint | Copy from the provider's official docs |
| Model Name | Exact model identifier | Verify against the current provider model list |
| OpenAI-compatible endpoint | API style used by many gateways | Path may include `/v1`, refer to the official documentation |
| Anthropic-compatible endpoint | API style expected by some Claude-compatible tools | Endpoint may be different, refer to the official documentation |

Maintenance workflow:

1. Open the provider's official documentation.
2. Find the current Base URL.
3. Find the current Model Name.
4. Update CC Switch.
5. Apply / Switch.
6. Restart Claude Code.
7. Test a short prompt.

> Note: Model names for DeepSeek, Qwen, GLM, Kimi, and other providers may change. Do not rely on old tutorials as permanent truth.

## 8. Updating Claude Code

Guidelines:

- Check the official Claude Code Setup documentation first.
- Use the update method recommended by Anthropic.
- Save work and close active Claude Code sessions before updating.
- Verify after updating.

Check version:

```powershell
claude --version
```

> Note: This guide intentionally does not provide a universal update command. Update behavior can change, so refer to the official documentation.

## 9. Updating Git

Recommended source:

[https://git-scm.com/download/win](https://git-scm.com/download/win)

General maintenance:

1. Download the latest Git for Windows installer from the official site.
2. Run the installer and follow the official prompts.
3. Reopen the terminal.
4. Verify:

```powershell
git --version
```

## 10. Updating CC Switch

Recommended sources:

- [https://ccswitch.io/](https://ccswitch.io/)
- [https://github.com/farion1231/cc-switch/releases](https://github.com/farion1231/cc-switch/releases)

Before updating:

| Step | Why |
| --- | --- |
| Back up provider settings | Avoid losing Base URL and model names |
| Redact API keys in screenshots | Avoid credential leakage |
| Close Claude Code | Prevent stale environment values |
| Download only from official sources | Avoid fake installers |

After updating:

1. Open CC Switch.
2. Confirm providers still exist.
3. Confirm the intended provider is selected.
4. Apply / Switch again if needed.
5. Restart Claude Code.
6. Test a model response.

## 11. Backing Up and Restoring Configuration

Recommended backup folder:

```text
C:\AI-Tools\Backup\
```

Back up:

| Item | Store in plaintext? | Notes |
| --- | --- | --- |
| Provider name | Yes | Example: DeepSeek |
| Base URL | Yes | Internal documentation is acceptable |
| Model Name | Yes | Helps restore the provider |
| API Key | No | Store only where it is kept, not the key itself |
| CC Switch screenshots | Yes, if redacted | Mask keys before sharing |
| Claude Code settings | Yes, if no secrets | Check before committing |
| Project folders | Yes | Use Git for important projects |

Backup template:

```markdown
# Provider Backup Template

## Provider Name
DeepSeek

## Base URL
Refer to the official documentation

## Model Name
Refer to the official documentation

## API Key
Do not store it here. Record only where it is managed.

## Notes
Used for Claude Code coding tasks.
```

Restore workflow:

1. Install Git for Windows.
2. Install Claude Code.
3. Install CC Switch.
4. Restore provider settings.
5. Enter a fresh API Key.
6. Apply / Switch.
7. Restart Claude Code.
8. Test file access and model response.

## 12. Troubleshooting Table

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| `claude` is not recognized | PATH not refreshed or installation failed | Reopen terminal, check installation, reinstall if needed |
| `git` is not recognized | Git is not installed | Install Git for Windows |
| `irm` is not recognized | PowerShell command used in CMD | Use PowerShell |
| `&&` fails | CMD command used in PowerShell | Use CMD or split into separate commands |
| API Key error | Key is wrong, expired, or leaked | Regenerate the key |
| `model not found` | Wrong or outdated model name | Check official model docs |
| 401 | Invalid API key | Check key and authentication style |
| 403 | No permission or insufficient balance | Check account permissions and billing |
| 404 | Wrong Base URL or model name | Check endpoint and model name |
| 429 | Rate limit or quota issue | Reduce request rate or check balance |
| 500 | Provider service error | Retry later or use another provider |
| Switching does not apply | Provider not applied or Claude Code not restarted | Apply / Switch, then restart Claude Code |
| Chat works but coding tools fail | Tool calling incompatibility | Try a coding model or compatible endpoint |
| Responses are slow | Network, provider load, or rate limit | Check network and try again later |
| Non-English or space-containing path fails | Path parsing or encoding issue | Use a simple English path |

## 13. Diagnostic Flow

### Step 1: Can Claude Code start?

```powershell
claude --version
claude
```

If not:

- Check installation.
- Check PATH.
- Reopen the terminal.
- Reinstall or repair using official documentation.

### Step 2: Is Git working?

```powershell
git --version
```

If not:

- Install Git for Windows.
- Check Git Bash path.
- Configure `CLAUDE_CODE_GIT_BASH_PATH` if needed.

### Step 3: Is the model endpoint working?

Check:

- API Key.
- Base URL.
- Model Name.
- Account balance.
- Provider service status.

### Step 4: Did CC Switch apply the provider?

Check:

- Current provider.
- Apply / Switch status.
- Whether Claude Code was restarted.
- Whether old environment variables override the new provider.

### Step 5: Is it a model capability issue?

Common signs:

- Chat works but file edits fail.
- Tool calls fail.
- Commands are not handled correctly.
- Code quality is poor.

Fixes:

- Try a stronger coding model.
- Try an Anthropic-compatible endpoint if the provider supports one.
- Compare with official Claude.
- Keep one stable fallback provider.

## 14. Daily Usage Rules

1. Keep each project in its own folder.
2. Avoid putting projects on the Desktop.
3. Use short English paths.
4. Do not put API keys inside project files.
5. Do not send API keys to anyone.
6. Initialize Git before serious coding work.
7. Back up important projects before large changes.
8. Read high-risk command approvals carefully.
9. Do not blindly approve file deletion commands.
10. Restart Claude Code after switching providers.

Recommended layout:

```text
C:\AI-Tools\
├── Projects\
│   ├── python-demo\
│   ├── matlab-demo\
│   └── web-demo\
├── Docs\
└── Backup\
```

## 15. Weekly Maintenance Checklist

- [ ] Check `claude --version`
- [ ] Check `git --version`
- [ ] Confirm CC Switch opens
- [ ] Confirm common providers still respond
- [ ] Check API balance
- [ ] Check for model name changes
- [ ] Check whether CC Switch has a new release
- [ ] Back up important configuration
- [ ] Clean up throwaway test projects
- [ ] Confirm no API key was exposed

## 16. Support Request Template

```text
Windows version:
Windows 10 / Windows 11

Claude Code version:
Output of claude --version:

Git version:
Output of git --version:

Terminal used:
PowerShell / CMD / Git Bash

Provider:
DeepSeek / Qwen / GLM / Kimi / SiliconFlow / OpenRouter / Other

Base URL:
Send only the domain or endpoint. Do not send the API key.

Model name:
Example: deepseek-chat

Error screenshot:
Please redact the API key.

Problem description:
When did it start?
Was it working before?
Did you update any software?
Did you switch providers recently?
```

> Note: Never send a full API key. Redact screenshots before sharing. Do not paste terminal output that contains secrets.

## 17. Minimal Health Check

PowerShell:

```powershell
git --version
claude --version
echo $env:ANTHROPIC_BASE_URL
claude
```

Inside Claude Code:

```text
Create health_check.md with the content "environment is healthy".
```

If the file is created successfully, the basics are working: Claude Code starts, the project folder is writable, the model responds, and the environment is ready for normal use. If it fails, follow the troubleshooting table and diagnostic flow above.
