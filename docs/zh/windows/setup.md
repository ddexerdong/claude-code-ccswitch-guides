# Windows 安装与验证指令速查表

这是一份面向 Windows 用户的快速安装与验证指南，只保留最常用的 Git、Node.js、Claude Code 安装和检查命令。

> 注意：Claude Code 官方当前支持 Windows 原生 PowerShell / CMD，也支持 Git Bash 和 WSL。Git Bash 推荐安装，因为 Claude Code 在 Windows 上常会用它执行类 Unix 命令。具体安装方式和支持情况以 [Claude Code 官方 Setup 文档](https://code.claude.com/docs/en/setup) 为准。

## 需要用到的网站

| 工具 | 网站 | 用途 |
| --- | --- | --- |
| Git for Windows | [https://git-scm.com/download/win](https://git-scm.com/download/win) | 下载 Git 和 Git Bash |
| Node.js | [https://nodejs.org/](https://nodejs.org/) | 下载 Node.js LTS |
| Claude Code Docs | [https://code.claude.com/docs/](https://code.claude.com/docs/) | 查看 Claude Code 官方文档 |
| Claude Code Setup | [https://code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup) | 查看 Windows 安装命令 |
| Anthropic Console | [https://console.anthropic.com/](https://console.anthropic.com/) | 管理 API Key |
| CC Switch | [https://ccswitch.io/](https://ccswitch.io/) | 如需切换模型，可下载 CC Switch |

## 快速安装与验证指南

### Git

安装方式一：下载安装包。

打开 Git for Windows 官网，下载 `.exe` 安装包并安装：

[https://git-scm.com/download/win](https://git-scm.com/download/win)

安装方式二：使用 WinGet。

```powershell
winget install --id Git.Git -e --source winget
```

验证指令：

```powershell
git --version
```

正常会输出类似：

```text
git version 2.54.0.windows.1
```

注意事项：

- 安装时建议勾选或保留 Add to PATH 相关选项。
- 安装成功后必须重新打开 PowerShell / CMD / Git Bash，否则可能提示找不到命令。
- Git Bash 常见路径是 `C:\Program Files\Git\bin\bash.exe`。

### Node.js

安装方式：

1. 打开 Node.js 官网：[https://nodejs.org/](https://nodejs.org/)
2. 下载 LTS 版本 `.msi` 安装包。
3. 运行安装程序。
4. 安装时确认 Add to PATH 相关选项已启用。

验证指令：

```powershell
node -v
npm -v
```

### Claude Code

推荐方式一：官方 Windows 安装器。

PowerShell：

```powershell
irm https://claude.ai/install.ps1 | iex
```

CMD：

```cmd
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

WinGet：

```powershell
winget install Anthropic.ClaudeCode
```

可选方式二：npm 安装。

如果你已经安装 Node.js，也可以使用 npm 方式。此方式以官方文档说明为准。

```bash
npm install -g @anthropic-ai/claude-code
```

验证指令：

```powershell
claude --version
```

或者运行一次简单测试：

```powershell
claude "Hello"
```

启动交互模式：

```powershell
claude
```

登录：

```text
/login
```

注意事项：

- Windows 原生 PowerShell / CMD 可以安装和启动 Claude Code。
- 如果命令执行、路径、Shell 行为异常，优先安装 Git for Windows，并尝试在 Git Bash 中运行。
- 如果你的项目在 Linux 环境里，建议使用 WSL，并在 WSL Terminal 中安装和运行 Claude Code。
- 运行时需要稳定网络；如果使用 API 方式，需要配置有效 API Key。
- 不要把 API Key 发给别人，也不要提交到 GitHub。

## 避坑小贴士

### 1. 安装后提示“不是内部或外部命令”

大多数情况是 PATH 没刷新。

处理方法：

1. 关闭当前 PowerShell / CMD / Git Bash。
2. 重新打开一个新终端。
3. 再运行验证命令。

```powershell
git --version
node -v
npm -v
claude --version
```

### 2. PowerShell 和 CMD 命令不要混用

PowerShell 安装 Claude Code：

```powershell
irm https://claude.ai/install.ps1 | iex
```

CMD 安装 Claude Code：

```cmd
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

如果 `irm` 报错，你可能在 CMD。  
如果 `&&` 报错，你可能在 PowerShell。

### 3. Claude Code 在 CMD 中异常

Claude Code 官方支持 Windows 原生环境，但不同机器上的 Shell、PATH、Git Bash、权限配置可能不同。

建议排查顺序：

1. 重新打开 CMD。
2. 改用 PowerShell 测试。
3. 安装 Git for Windows 后改用 Git Bash 测试。
4. 如果项目本来就在 Linux 工具链里，改用 WSL。

### 4. 最小自检命令

```powershell
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

> 注意：不要从不明网盘、私信链接、广告站下载 CC Switch。任何 API Key、Token、Base URL 都不要公开。

如果安装过程中遇到报错，把终端输出发给技术支持即可。截图前请打码 API Key。
