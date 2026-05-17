# Maintenance Guide: Claude Code + CC Switch + Third-Party Models on macOS

> Note: This guide is for ongoing maintenance and customer self-checks. It does not run any install, update, delete, or reset command. For official tools, settings fields, endpoints, and model names, refer to the official documentation.

## Useful Maintenance Websites

| Website | Purpose |
| --- | --- |
| [Claude Code Documentation](https://code.claude.com/docs/) | Installation, configuration, permissions, updates, environment variables, and troubleshooting. |
| [Claude Code Quickstart](https://code.claude.com/docs/en/quickstart) | Basic startup, login, and common commands. |
| [Claude Code Setup](https://code.claude.com/docs/en/setup) | macOS installation methods, system requirements, verification, and update notes. |
| [Claude Code Environment Variables](https://code.claude.com/docs/en/env-vars) | `ANTHROPIC_API_KEY`, `ANTHROPIC_BASE_URL`, and related variables. |
| [Claude Code Settings](https://code.claude.com/docs/en/settings) | `settings.json`, `/config`, user settings, and project settings. |
| [Anthropic Console](https://console.anthropic.com/) | Anthropic API key management. |
| [CC Switch Website](https://ccswitch.io/) | Official CC Switch download and product information. |
| [CC Switch GitHub](https://github.com/farion1231/cc-switch) | Source code, documentation, updates, and security notes. |
| [CC Switch Releases](https://github.com/farion1231/cc-switch/releases) | Manual downloads and release notes. |
| [Homebrew](https://brew.sh/) | Maintain macOS development tools. |
| [Git](https://git-scm.com/) | Git documentation and downloads. |
| [VS Code](https://code.visualstudio.com/) | Code editor and workspace. |
| [Python for macOS](https://www.python.org/downloads/macos/) | Python downloads and documentation. |
| [Node.js](https://nodejs.org/) | Node.js LTS downloads and documentation. |
| [DeepSeek Platform](https://platform.deepseek.com/) | API keys, billing, model access, and account status. |
| [DeepSeek API Docs](https://api-docs.deepseek.com/) | Base URL, model names, and API format. |
| [Alibaba Cloud Bailian / DashScope](https://bailian.console.aliyun.com/) | Qwen API keys, model access, and usage. |
| [DashScope Documentation](https://help.aliyun.com/zh/model-studio/) | OpenAI-compatible API, model names, and calling format. |
| [Zhipu AI](https://open.bigmodel.cn/) | GLM API keys and model access. |
| [Kimi / Moonshot](https://platform.moonshot.cn/) | Kimi API keys and model access. |
| [SiliconFlow](https://siliconflow.cn/) | API keys for Chinese and open-source models. |
| [OpenRouter](https://openrouter.ai/) | Multi-model routing API. |
| [New API](https://github.com/Calcium-Ion/new-api) | Self-hosted or managed OpenAI-compatible gateway. |
| [One API](https://github.com/songquanpeng/one-api) | Self-hosted or managed OpenAI-compatible gateway. |

> Note: Download CC Switch only from the official website or GitHub Releases. Do not use unknown relay services, repackaged installers, or private download links.

## 1. What This Environment Includes

| Component | Plain-English meaning | What to maintain |
| --- | --- | --- |
| Claude Code | AI coding workspace | Startup, login, file access, command execution |
| Homebrew | macOS package manager | `brew` health and package updates |
| Git | Version control | `git` availability |
| Node.js / Python | Common development runtimes | Version checks and project compatibility |
| CC Switch | Provider configuration and model switcher | Provider settings and switch behavior |
| API Key | Secret used to call a model API | Validity, rotation, and leakage prevention |
| Base URL | Model API endpoint | Correct endpoint and path |
| Model Name | Exact model identifier | Current availability and account permissions |
| Project folder | Claude Code working directory | Clean path, permissions, and backups |

## 2. Quick Health Check Before Use

```bash
brew --version
git --version
node --version
python3 --version
claude --version
echo $ANTHROPIC_API_KEY
echo $ANTHROPIC_BASE_URL
```

Expected results:

| Check | Expected result |
| --- | --- |
| Homebrew | Shows a version |
| Git | Shows a Git version |
| Node.js | Shows a Node.js version |
| Python | Shows a Python 3 version |
| Claude Code | Shows a Claude Code version |
| API Key | Present when using API-based providers; may be empty for official login |
| Base URL | Present when using third-party providers; may be empty for official login |

> Note: `echo $ANTHROPIC_API_KEY` may display a secret. Do not screenshot or forward the output unless the key is fully redacted.

## 3. Checking Claude Code

Run:

```bash
claude --version
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

Healthy behavior:

- Claude Code starts.
- `test.md` is created.
- The current project folder can be read and written.
- Simple commands can run.

Common issues:

| Issue | What to do |
| --- | --- |
| `claude: command not found` | Reopen Terminal, check PATH, and refer to the official setup docs. |
| Cannot log in | Check network, browser redirect, and account permissions. |
| Cannot read/write files | Move the project to `~/AI-Tools/Projects/` and test again. |
| Too many permission prompts | Read each permission prompt and approve only safe operations. |

## 4. Checking Homebrew

Check Homebrew:

```bash
brew --version
```

Update Homebrew metadata:

```bash
brew update
```

Upgrade installed packages:

```bash
brew upgrade
```

Common issues:

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| `brew: command not found` | Homebrew is not installed or PATH is wrong | Install Homebrew from the official site and fix PATH. |
| Updates are slow | Network or mirror issue | Check the network and retry later. |
| Permission errors | Homebrew directory permissions are wrong | Refer to the official Homebrew documentation. |

## 5. Checking Git

```bash
git --version
```

If Git is not working:

1. Confirm Homebrew works.
2. Confirm Git is installed.
3. Reopen Terminal.
4. Refer to the Git or Homebrew documentation if needed.

## 6. Checking Node.js and Python

```bash
node --version
python3 --version
```

If a project requires a specific runtime version, follow that project's README. Do not blindly upgrade production project runtimes.

## 7. Checking CC Switch

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

Validation:

```bash
cd ~/AI-Tools/Projects/demo
claude
```

Inside Claude Code:

```text
Please confirm in one sentence that the current model endpoint is responding.
```

Expected: a normal reply with no API Key error, Base URL error, `model not found`, 401, 403, 404, or 429.

## 8. Maintaining API Keys

Replace an API key when:

- The key was exposed.
- The key expired.
- The provider account changed.
- Billing or permissions changed.
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

> Note: Never store API keys in README files, Git repositories, screenshots, support tickets, or shared notes. If a key may have leaked, revoke it immediately.

## 9. Maintaining Base URLs and Model Names

| Item | Meaning | Maintenance rule |
| --- | --- | --- |
| Base URL | API endpoint | Copy from the provider's official docs |
| Model Name | Exact model identifier | Verify against the current provider model list |
| OpenAI-compatible endpoint | API style used by many gateways | Path may include `/v1`; refer to the official documentation |
| Anthropic-compatible endpoint | API style expected by some Claude-compatible tools | Endpoint may differ; refer to the official documentation |

Workflow:

1. Open the provider's official documentation.
2. Find the current Base URL.
3. Find the current Model Name.
4. Update CC Switch.
5. Apply / Switch.
6. Restart Claude Code.
7. Test a short prompt.

## 10. Updating Claude Code

Check the official Setup documentation before updating:

[https://code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup)

Version check:

```bash
claude --version
```

If you installed with Homebrew, the update command depends on the cask you installed. Common examples include:

```bash
brew upgrade claude-code
```

or:

```bash
brew upgrade claude-code@latest
```

> Note: Claude Code update behavior can change. Native installs, Homebrew installs, and managed enterprise installs may behave differently. Refer to the official documentation.

## 11. Updating CC Switch

If installed with Homebrew:

```bash
brew upgrade --cask cc-switch
```

If installed manually:

1. Open [CC Switch Releases](https://github.com/farion1231/cc-switch/releases).
2. Download the latest macOS build.
3. Back up provider settings first.
4. Install the new version.
5. Confirm providers still exist.
6. Re-test provider switching.

> Note: Use only the official website or GitHub Releases.

## 12. Updating Homebrew / Git / Node.js / Python

Update Homebrew metadata:

```bash
brew update
```

Upgrade packages:

```bash
brew upgrade
```

Check versions:

```bash
git --version
node --version
python3 --version
```

> Note: If a project depends on a specific Node.js or Python version, read the project documentation before upgrading.

## 13. Backing Up and Restoring Configuration

Recommended backup folder:

```text
~/AI-Tools/Backup/
```

Back up:

| Item | Store in plaintext? | Notes |
| --- | --- | --- |
| Provider name | Yes | Example: DeepSeek |
| Base URL | Yes | Safe for internal docs, but keep it controlled |
| Model Name | Yes | Helps restore providers |
| API Key | No | Record only where it is managed |
| CC Switch screenshots | Yes, if redacted | Mask all secrets |
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

1. Install Homebrew.
2. Install Git, Claude Code, and CC Switch.
3. Restore provider settings.
4. Enter a fresh API Key.
5. Apply / Switch.
6. Restart Claude Code.
7. Test file access and model response.

## 14. Troubleshooting Table

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| `brew: command not found` | Homebrew is missing or PATH is wrong | Install Homebrew or fix PATH. |
| `claude: command not found` | Claude Code is missing or PATH is stale | Reopen Terminal and check official setup steps. |
| `git: command not found` | Git is missing | Install Git with Homebrew or official installer. |
| API Key error | Key is wrong, expired, or leaked | Regenerate the key. |
| 401 | Invalid API key | Check key and authentication style. |
| 403 | No permission or insufficient balance | Check account permissions and billing. |
| 404 | Wrong Base URL or model name | Check endpoint and model name. |
| 429 | Rate limit or quota issue | Reduce request rate or check balance. |
| 500 | Provider service error | Retry later or use another provider. |
| `model not found` | Wrong or outdated model name | Check official model docs. |
| CC Switch does not apply | Provider not applied or Claude Code not restarted | Apply / Switch, then restart Claude Code. |
| App cannot be opened | macOS security restrictions | Confirm source and allow in Privacy & Security. |
| Non-English path fails | Path parsing or encoding issue | Use a short English path. |
| Chat works but file edits fail | Tool calling incompatibility | Try a coding model or official Claude for comparison. |

## 15. Diagnostic Flow

### Step 1: Can Claude Code start?

```bash
claude --version
claude
```

If not, check installation, PATH, network, and the official documentation.

### Step 2: Are Homebrew and Git working?

```bash
brew --version
git --version
```

Fix Homebrew or Git first if either fails.

### Step 3: Is the model endpoint working?

Check:

- API Key.
- Base URL.
- Model Name.
- Account balance.
- Provider status.

### Step 4: Did CC Switch apply the provider?

Check:

- Current provider.
- Apply / Switch status.
- Whether Claude Code was restarted.
- Whether old environment variables override the new provider.

### Step 5: Is it a model capability issue?

Common signs:

- Chat works but tool calls fail.
- Responses work but file edits fail.
- Code quality is poor.
- Long tasks frequently fail.

Fixes:

- Try a stronger coding model.
- Use a provider-recommended compatible endpoint.
- Compare with official Claude.
- Keep one stable fallback provider.

## 16. Daily Usage Rules

1. Keep each project in its own folder.
2. Avoid placing projects on the Desktop.
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
~/AI-Tools/
├── Projects/
│   ├── python-demo/
│   ├── web-demo/
│   └── docs-demo/
├── Docs/
└── Backup/
```

## 17. Weekly Maintenance Checklist

- [ ] Check `brew --version`
- [ ] Check `git --version`
- [ ] Check `node --version`
- [ ] Check `python3 --version`
- [ ] Check `claude --version`
- [ ] Confirm CC Switch opens
- [ ] Confirm common providers still respond
- [ ] Check API balance
- [ ] Check for model name changes
- [ ] Back up important configuration
- [ ] Confirm no API key was exposed

## 18. Support Request Template

```text
macOS version:

Mac chip:
Apple Silicon / Intel

Claude Code version:
Output of claude --version:

Homebrew version:
Output of brew --version:

Git version:
Output of git --version:

Provider:
DeepSeek / Qwen / GLM / Kimi / SiliconFlow / OpenRouter / Other

Base URL:
Send only the endpoint or domain. Do not send the API key.

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

## 19. Minimal Health Check

```bash
brew --version
git --version
claude --version
echo $ANTHROPIC_BASE_URL
claude
```

Inside Claude Code:

```text
Create health_check.md with the content "environment is healthy".
```

If the file is created successfully, the basics are working: Claude Code starts, the project folder is writable, the model responds, and the environment is ready for normal use. If it fails, follow the troubleshooting table and diagnostic flow above.
