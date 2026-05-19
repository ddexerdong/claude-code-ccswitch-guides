# macOS 安装与验证指令速查表

这是一份面向 macOS 用户的快速安装与验证指南，只保留最常用的 Git、Node.js、Claude Code 安装和检查命令。

> 注意：Claude Code 在 macOS 上可以直接在 Terminal.app 或 iTerm2 中运行。具体安装方式和支持情况以 [Claude Code 官方 Setup 文档](https://code.claude.com/docs/en/setup) 为准。

## 需要用到的网站

| 工具 | 网站 | 用途 |
| --- | --- | --- |
| Homebrew | [https://brew.sh/](https://brew.sh/) | 安装和管理 macOS 开发工具 |
| Git | [https://git-scm.com/](https://git-scm.com/) | 下载 Git 或查看文档 |
| Node.js | [https://nodejs.org/](https://nodejs.org/) | 下载 Node.js LTS |
| Claude Code Docs | [https://code.claude.com/docs/](https://code.claude.com/docs/) | 查看 Claude Code 官方文档 |
| Claude Code Setup | [https://code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup) | 查看 macOS 安装命令 |
| Anthropic Console | [https://console.anthropic.com/](https://console.anthropic.com/) | 管理 API Key |
| CC Switch | [https://ccswitch.io/](https://ccswitch.io/) | 如需切换模型，可下载 CC Switch |

## 快速安装与验证指南

### Homebrew

如果还没有 Homebrew，先安装：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

验证：

```bash
brew --version
```

Apple Silicon Mac 常见路径：

```text
/opt/homebrew/bin/brew
```

Intel Mac 常见路径：

```text
/usr/local/bin/brew
```

如果 `brew` 找不到，Apple Silicon Mac 通常需要执行：

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

### Git

安装方式一：使用 Homebrew。

```bash
brew install git
```

安装方式二：下载官方安装程序。

[https://git-scm.com/](https://git-scm.com/)

验证指令：

```bash
git --version
```

示例输出：

```text
git version 2.42.0
```

说明：

- macOS 可能自带旧版 Git。
- 如果想使用较新的 Git，建议通过 Homebrew 安装或升级。

### Node.js

安装方式一：使用 Homebrew。

```bash
brew install node
```

安装方式二：下载官方 LTS 安装包。

[https://nodejs.org/](https://nodejs.org/)

安装方式三：使用版本管理器，例如 `n` 或 `nvm`。

验证指令：

```bash
node -v
npm -v
```

### Claude Code

推荐方式一：官方安装脚本。

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

推荐方式二：Homebrew。

```bash
brew install --cask claude-code
```

可选方式三：npm 安装。

如果你已经安装 Node.js，也可以使用 npm 方式。此方式以官方文档说明为准。

```bash
npm install -g @anthropic-ai/claude-code
```

验证指令：

```bash
claude --version
```

或者运行一次简单测试：

```bash
claude "Hello"
```

启动交互模式：

```bash
claude
```

登录：

```text
/login
```

说明：

- macOS 上可以直接在系统终端中运行 Claude Code。
- 不需要 WSL。
- 运行时需要稳定网络；如果使用 API 方式，需要配置有效 API Key。
- 不要把 API Key 发给别人，也不要提交到 GitHub。

## 小贴士

### 1. 权限问题

如果 `npm install -g` 报权限错误，不建议长期依赖 `sudo npm install -g`。

可以优先改用 Homebrew 安装 Node.js，或者按 npm 官方建议修复全局安装目录权限。

你也可以临时检查 npm 全局路径：

```bash
npm config get prefix
```

### 2. 终端路径刷新

安装完成后，如果命令找不到，先重新打开 Terminal。

如果你使用 zsh，也可以执行：

```bash
source ~/.zshrc
```

或：

```bash
source ~/.zprofile
```

### 3. 最小自检命令

```bash
brew --version
git --version
node -v
npm -v
claude --version
```

如果以上命令都能输出版本号，基础环境基本正常。

## CC Switch 简短说明

如果你还需要用 CC Switch 切换 DeepSeek / Qwen / GLM / Kimi / SiliconFlow / OpenRouter 等模型，请从官方来源下载：

- 官网：[https://ccswitch.io/](https://ccswitch.io/)
- GitHub：[https://github.com/farion1231/cc-switch](https://github.com/farion1231/cc-switch)
- Releases：[https://github.com/farion1231/cc-switch/releases](https://github.com/farion1231/cc-switch/releases)

Homebrew 安装方式：

```bash
brew tap farion1231/ccswitch
brew install --cask cc-switch
```

> 注意：不要从不明网盘、私信链接、广告站下载 CC Switch。任何 API Key、Token、Base URL 都不要公开。

如果安装过程中遇到报错，把终端输出发给技术支持即可。截图前请打码 API Key。
