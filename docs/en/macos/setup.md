# macOS Quick Install and Verification Cheat Sheet

This is a short macOS setup guide for Homebrew, Git, Node.js, Claude Code, and CC Switch. It keeps only the commands and checks most users need.

> Note: Claude Code can run directly in Terminal.app or iTerm2 on macOS. For the latest installer behavior, refer to the [official Claude Code Setup documentation](https://code.claude.com/docs/en/setup).

## Useful Websites

| Tool | Website | Purpose |
| --- | --- | --- |
| Homebrew | [https://brew.sh/](https://brew.sh/) | Install and manage macOS developer tools |
| Git | [https://git-scm.com/](https://git-scm.com/) | Download Git or read Git documentation |
| Node.js | [https://nodejs.org/](https://nodejs.org/) | Download Node.js LTS |
| Claude Code Docs | [https://code.claude.com/docs/](https://code.claude.com/docs/) | Read the official Claude Code documentation |
| Claude Code Setup | [https://code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup) | Check the latest macOS installation commands |
| Anthropic Console | [https://console.anthropic.com/](https://console.anthropic.com/) | Manage Anthropic API keys |
| CC Switch | [https://ccswitch.io/](https://ccswitch.io/) | Download CC Switch if you need model switching |

## Quick Install and Verification Guide

### Homebrew

If Homebrew is not installed yet, install it first:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Verify:

```bash
brew --version
```

Common Apple Silicon path:

```text
/opt/homebrew/bin/brew
```

Common Intel Mac path:

```text
/usr/local/bin/brew
```

If `brew` is not found on Apple Silicon, run:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

### Git

Option 1: install with Homebrew.

```bash
brew install git
```

Option 2: download the official installer.

[https://git-scm.com/](https://git-scm.com/)

Verify:

```bash
git --version
```

Expected output looks like this:

```text
git version 2.42.0
```

Notes:

- macOS may include an older Git version.
- If you want a newer Git version, install or upgrade it with Homebrew.

### Node.js

Option 1: install with Homebrew.

```bash
brew install node
```

Option 2: download the official LTS installer.

[https://nodejs.org/](https://nodejs.org/)

Option 3: use a version manager such as `n` or `nvm`.

Verify:

```bash
node -v
npm -v
```

### Claude Code

Recommended option 1: official installer.

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Recommended option 2: Homebrew.

```bash
brew install --cask claude-code
```

Optional option 3: npm installation.

If Node.js is already installed, you can also use npm. Refer to the official documentation for the latest npm support notes.

```bash
npm install -g @anthropic-ai/claude-code
```

Verify:

```bash
claude --version
```

Or run a simple test:

```bash
claude "Hello"
```

Start interactive mode:

```bash
claude
```

Login inside Claude Code:

```text
/login
```

Notes:

- Claude Code runs directly in Terminal.app or iTerm2 on macOS.
- WSL is not needed on macOS.
- A stable network is required. API-based usage also requires a valid API key.
- Never share API keys, tokens, or private Base URLs. Do not commit them to GitHub.

## Tips

### 1. npm Permission Errors

If `npm install -g` fails with a permission error, avoid relying on `sudo npm install -g` as a long-term fix.

Prefer installing Node.js with Homebrew, or follow npm's official guidance for fixing the global install directory.

You can check the npm global prefix with:

```bash
npm config get prefix
```

### 2. Refresh Terminal PATH

After installation, if a command is not found, close and reopen Terminal.

If you use zsh, you can also run:

```bash
source ~/.zshrc
```

Or:

```bash
source ~/.zprofile
```

### 3. Minimal Health Check

```bash
brew --version
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

Homebrew installation:

```bash
brew tap farion1231/ccswitch
brew install --cask cc-switch
```

> Note: Do not download CC Switch from random cloud-drive links, private-message links, ad sites, or repackaged installers. Never expose API keys, tokens, or Base URLs.

If installation fails, send the terminal error output to technical support. Mask any API key before sharing screenshots.
