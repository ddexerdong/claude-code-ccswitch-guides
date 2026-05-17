# Windows 系统配置 Claude Code，并使用 CC Switch / ccswitch 切换国产模型完整教程

> 注意：本文是一份 Windows 安装与配置教程，只生成操作说明，不会替你执行任何安装命令。实际安装、登录、充值、创建 API Key、修改系统环境变量前，请确认你正在访问官方网站，并以官方文档为准。

## 开始前先理解三件事

### Claude Code 是什么

Claude Code 是 Anthropic 提供的 AI 编程助手。它可以在命令行中运行，帮助用户：

| 能力 | 说明 |
| --- | --- |
| 读项目 | 理解当前目录里的代码、文档和配置 |
| 改代码 | 按你的要求修改文件、补充测试、修复错误 |
| 运行命令 | 调用 Git、构建、测试、脚本等命令 |
| 辅助开发 | 做需求拆解、代码审查、重构建议和问题排查 |

### DeepSeek / Qwen / GLM / Kimi 是什么

DeepSeek、Qwen、GLM、Kimi 可以理解为不同厂商或平台提供的 AI 模型。它们就像不同的“AI 大脑”，能力、价格、接口地址、模型名称、上下文长度、工具调用兼容性都可能不同。

### CC Switch 是什么

CC Switch / ccswitch 是一个用来管理不同 AI 模型配置的桌面工具。它可以减少手动修改环境变量、配置文件和 Base URL 的次数，让用户通过界面添加、启用、切换不同 Provider。

三者关系可以这样理解：

| 组件 | 类比 | 作用 |
| --- | --- | --- |
| Claude Code | AI 开发工作台 | 负责读项目、改代码、运行命令 |
| DeepSeek / Qwen / GLM / Kimi | 可切换的 AI 大脑 | 提供模型推理能力 |
| CC Switch | 模型切换器 / 配置管理器 | 管理 API Key、Base URL、模型名和目标工具配置 |

## 重要安全提醒

> 注意：API Key、Base URL、Token、Bearer Token、Custom Headers 都属于敏感配置。不要发到微信群、论坛、公开 GitHub 仓库、截图、工单附件或陌生人提供的网页里。

> 注意：本文不推荐不明来源的低价中转站，不引导用户去非官方下载站，不保证第三方接口与 Claude Code 的所有功能完全兼容。涉及第三方 Provider、OpenAI Compatible 网关、New API、One API、国产模型平台时，接口格式、模型名、鉴权方式必须以对应平台官方文档为准。

## 需要用到的网站

只需要根据自己实际使用的模型平台注册对应平台，不需要把下面所有网站都注册一遍。比如只使用官方 Claude Code，就只需要 Claude 账号或 Anthropic Console；只使用 DeepSeek，就只需要 DeepSeek 平台；只使用 Qwen，就只需要阿里云百炼 / DashScope。

| 序号 | 网站 | 用途 |
| --- | --- | --- |
| 1 | [Claude Code 官方文档](https://code.claude.com/docs/) | 查看 Claude Code 安装、配置、权限、Windows 环境说明。 |
| 2 | [Claude Code 安装文档](https://code.claude.com/docs/en/setup) | 查看 Windows 安装方式、Git Bash、PowerShell/CMD 区别、环境变量说明。 |
| 3 | [Claude Code 快速开始](https://code.claude.com/docs/en/quickstart) | 查看 `claude` 命令、登录、启动项目、基本使用。 |
| 4 | [Anthropic Console](https://console.anthropic.com/) | 申请或管理 Anthropic API Key。 |
| 5 | [CC Switch 官方网站](https://ccswitch.io/) | 下载和了解 CC Switch。 |
| 6 | [CC Switch GitHub 仓库](https://github.com/farion1231/cc-switch) | 查看源码、说明、Release、下载地址和安全提醒。 |
| 7 | [CC Switch Releases](https://github.com/farion1231/cc-switch/releases) | 下载 Windows 安装包。 |
| 8 | [Git for Windows](https://git-scm.com/download/win) | 安装 Git 和 Git Bash。 |
| 9 | [VS Code](https://code.visualstudio.com/) | 作为代码编辑器和项目管理工具。 |
| 10 | [Python 官网](https://www.python.org/downloads/windows/) | 安装 Python，给脚本、自动化、工具链使用。 |
| 11 | [Node.js 官网](https://nodejs.org/) | 部分前端/CLI 工具或 npm 工具可能需要。 |
| 12 | [DeepSeek 官方平台](https://platform.deepseek.com/) | 申请 DeepSeek API Key。 |
| 13 | [DeepSeek API 文档](https://api-docs.deepseek.com/) | 查看 API Base URL、模型名、调用格式。 |
| 14 | [阿里云百炼 / DashScope](https://bailian.console.aliyun.com/) | 申请 Qwen / 通义千问 API Key。 |
| 15 | [DashScope 文档](https://help.aliyun.com/zh/model-studio/) | 查看 Qwen 模型、OpenAI Compatible 接口、Base URL。 |
| 16 | [智谱 AI 开放平台](https://open.bigmodel.cn/) | 申请 GLM API Key。 |
| 17 | [月之暗面 Kimi 开放平台](https://platform.moonshot.cn/) | 申请 Kimi API Key。 |
| 18 | [硅基流动 SiliconFlow](https://siliconflow.cn/) | 申请国产/开源模型 API Key。 |
| 19 | [OpenRouter](https://openrouter.ai/) | 使用多模型聚合接口。 |
| 20 | [New API 项目](https://github.com/Calcium-Ion/new-api) | 自建或使用 OpenAI Compatible API 网关。 |
| 21 | [One API 项目](https://github.com/songquanpeng/one-api) | 自建或使用 OpenAI Compatible API 网关。 |

## 必备环境

| 环境 | 是否必须 | 作用 |
| --- | --- | --- |
| Windows 10/11 | 必须 | 运行 Claude Code |
| PowerShell / Windows Terminal | 必须 | 执行安装命令 |
| Git for Windows | 推荐必须 | 提供 Git 和 Git Bash |
| Claude Code | 必须 | AI 编程助手 |
| Claude 账号或 API Key | 至少一种 | 登录或调用模型 |
| 稳定网络 | 必须 | 下载和调用 API |

## 推荐环境

| 环境 | 作用 |
| --- | --- |
| VS Code | 编辑代码和文档 |
| Python 3.10+ | 自动化脚本、测试工具 |
| Node.js LTS | 部分 CLI 工具可能需要 |
| GitHub 账号 | 项目备份和版本管理 |
| Windows Terminal | 更好用的命令行 |

## 推荐目录结构

建议在 Windows 上建立一个简单英文路径，例如：

```text
C:\AI-Tools
├── ClaudeCode
├── CC-Switch
├── Projects
└── Docs\
```

建议原则：

| 建议 | 原因 |
| --- | --- |
| 不建议放桌面 | 桌面路径可能被 OneDrive 同步，权限和路径容易混乱 |
| 不建议中文路径 | 部分 CLI 工具、脚本、依赖可能对中文路径兼容不好 |
| 不建议路径有特殊符号 | 空格、括号、`#`、`&` 可能导致命令解析问题 |
| 尽量使用简单英文路径 | 更容易复制命令、排查问题、给团队复现 |

## 命令行基础说明

Windows 上常见三种终端：PowerShell、CMD、Git Bash。很多安装失败都不是软件问题，而是把某个终端的命令复制到了另一个终端里。

| 终端 | 提示符样子 | 适合命令 |
| --- | --- | --- |
| PowerShell | `PS C:\Users\xxx>` | `irm`、`setx`、`$env` |
| CMD | `C:\Users\xxx>` | `curl`、`&&`、`set` |
| Git Bash | `user@PC MINGW64 ~` | `ls`、`bash`、类 Linux 命令 |

> 注意：`irm` 是 PowerShell 命令，CMD 不能用。

> 注意：`&&` 在 CMD/Git Bash 常见，PowerShell 里可能报错。新版本 PowerShell 支持情况可能变化，但新手遇到报错时，优先确认自己在哪个终端。

> 注意：如果命令报错，先看终端提示符。看到 `PS C:\` 基本就是 PowerShell；看到 `C:\Users\xxx>` 基本就是 CMD；看到 `MINGW64` 基本就是 Git Bash。

## 官方 Claude Code 登录使用和 API / 中转 / 国产模型接口使用的区别

| 使用方式 | 需要什么 | 配置重点 | 适合场景 | 风险和注意事项 |
| --- | --- | --- | --- | --- |
| 官方 Claude Code 登录使用 | Claude Pro / Max / Team / Enterprise 或 Console 账号，具体以官方文档为准 | 安装 Claude Code 后运行 `claude`，按浏览器提示登录，或在 Claude Code 中使用 `/login` | 最简单、兼容性最好、权限和工具调用体验通常最稳定 | 需要账号有 Claude Code 使用权限；免费 Claude.ai 计划是否支持以官方文档为准 |
| Anthropic API Key 直连 | Anthropic Console API Key | `ANTHROPIC_API_KEY`，必要时使用官方 API 配置 | 企业、开发者、自动化脚本 | API Key 会产生费用，不要泄露 |
| API / 中转 / 国产模型接口 | 对应平台账号、API Key、Base URL、模型名 | `ANTHROPIC_BASE_URL`、`ANTHROPIC_AUTH_TOKEN`、`ANTHROPIC_CUSTOM_HEADERS`、CC Switch Provider 配置等 | 想切换 DeepSeek、Qwen、GLM、Kimi、SiliconFlow、OpenRouter 或自建网关 | 不同平台对工具调用、长上下文、流式输出、Anthropic Format 兼容程度不同；不确定配置必须以官方文档为准 |

> 注意：官方登录和自定义 API 接口不要混在一起排查。设置了 `ANTHROPIC_API_KEY`、`ANTHROPIC_AUTH_TOKEN` 或自定义 Base URL 后，Claude Code 可能优先使用这些配置。切回官方登录时，请检查环境变量和 CC Switch 当前 Provider。

## 安装 Git for Windows

下载网站：

[https://git-scm.com/download/win](https://git-scm.com/download/win)

### 安装步骤

1. 打开 Git for Windows 官网。
2. 下载 Windows 安装包。
3. 双击安装。
4. 新手可以使用默认选项。
5. 安装完成后重新打开 PowerShell、CMD 或 Git Bash。

### 验证 Git

PowerShell、CMD、Git Bash 都可以运行：

```powershell
git --version
```

正确现象：

```text
git version x.x.x.windows.x
```

### 验证 Git Bash

Git Bash 常见路径为：

```text
C:\Program Files\Git\bin\bash.exe
```

PowerShell 或 CMD 中验证：

```powershell
"C:\Program Files\Git\bin\bash.exe" --version
```

如果 Claude Code 找不到 Git Bash，可以在 Claude Code 的 `settings.json` 或项目配置中指定路径，具体配置位置和支持字段以 Claude Code 官方文档为准。

Windows 原始路径：

```text
C:\Program Files\Git\bin\bash.exe
```

JSON 中建议写成双反斜杠：

```json
{
  "env": {
    "CLAUDE_CODE_GIT_BASH_PATH": "C:\\Program Files\\Git\\bin\\bash.exe"
  }
}
```

> 注意：官方文档说明 Windows 上 `~/.claude` 通常对应 `%USERPROFILE%\.claude`。用户级配置常见位置可能是 `%USERPROFILE%\.claude\settings.json`，项目级配置可能是项目目录下的 `.claude\settings.json` 或 `.claude\settings.local.json`，具体以官方文档为准。

## 安装 Claude Code

官方文档：

- [Claude Code 安装文档](https://code.claude.com/docs/en/setup)
- [Claude Code 快速开始](https://code.claude.com/docs/en/quickstart)

> 注意：下面三种方式选择一种即可，不要三种都重复安装。安装命令需要用户自己在 Windows 终端中执行。

### 方式一：PowerShell 安装

适用终端：PowerShell 或 Windows Terminal 中的 PowerShell。

```powershell
irm https://claude.ai/install.ps1 | iex
```

如果提示 `irm` 不识别，说明你大概率在 CMD，不是在 PowerShell。

### 方式二：CMD 安装

适用终端：CMD。

```cmd
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

如果提示 `&&` 不是有效语句分隔符，说明你大概率在 PowerShell，不是在 CMD。

### 方式三：WinGet 安装

适用终端：PowerShell 或 CMD。

```powershell
winget install Anthropic.ClaudeCode
```

WinGet 安装如果失败，请检查 Windows 版本、Microsoft Store 的 App Installer、公司网络代理和管理员权限。具体以 Microsoft 和 Claude Code 官方文档为准。

### 安装完成后验证

重新打开终端，然后运行：

```powershell
claude --version
```

正确现象：

```text
Claude Code 版本号
```

启动 Claude Code：

```powershell
claude
```

如果当前版本支持 `doctor`，可以运行：

```powershell
claude doctor
```

> 注意：如果提示 `claude` 不是内部或外部命令，说明 PATH 可能没刷新。先关闭并重新打开终端；仍不行就重启电脑；还不行再重新安装或查看官方安装排错文档。

## Claude Code 基础使用

### 创建项目目录

PowerShell / CMD：

```cmd
mkdir C:\AI-Tools\Projects\demo
cd C:\AI-Tools\Projects\demo
```

Git Bash：

```bash
mkdir -p /c/AI-Tools/Projects/demo
cd /c/AI-Tools/Projects/demo
```

### 启动 Claude Code

```powershell
claude
```

### 登录

Claude Code 首次启动通常会引导浏览器登录。也可以在 Claude Code 交互界面输入：

```text
/login
```

常用命令：

```text
/help
/login
/model
/resume
```

### 基础测试

进入 Claude Code 后，可以输入这些自然语言测试：

```text
请解释当前目录结构。
```

```text
请创建 hello.md，内容为 hello claude。
```

```text
请运行 dir 查看当前目录。
```

退出 Claude Code 后，在 PowerShell 或 CMD 里查看：

```cmd
dir
```

如果看到 `hello.md`，说明基本读写正常。

## 环境变量配置

环境变量用于告诉 Claude Code 或相关工具使用哪个 API Key、Base URL、Token 或额外请求头。

> 注意：只有你明确需要 API Key、自定义接口、国产模型或中转网关时，才需要配置这些变量。只使用官方 Claude 登录时，通常先不要手动设置 API Key 和 Base URL，避免排查混乱。

### PowerShell 临时设置

临时设置只对当前 PowerShell 窗口有效，关闭窗口后失效。

```powershell
$env:ANTHROPIC_API_KEY="你的_API_Key"
$env:ANTHROPIC_BASE_URL="你的_Base_URL"
```

### PowerShell 查看变量

```powershell
echo $env:ANTHROPIC_API_KEY
echo $env:ANTHROPIC_BASE_URL
```

> 注意：查看变量会把 API Key 显示在屏幕上。不要截图，不要直播，不要在共享屏幕时展示。

### CMD 临时设置

```cmd
set ANTHROPIC_API_KEY=你的_API_Key
set ANTHROPIC_BASE_URL=你的_Base_URL
```

CMD 查看变量：

```cmd
echo %ANTHROPIC_API_KEY%
echo %ANTHROPIC_BASE_URL%
```

### Git Bash 临时设置

```bash
export ANTHROPIC_API_KEY="你的_API_Key"
export ANTHROPIC_BASE_URL="你的_Base_URL"
```

Git Bash 查看变量：

```bash
echo $ANTHROPIC_API_KEY
echo $ANTHROPIC_BASE_URL
```

### 永久设置用户环境变量

PowerShell 或 CMD 都可以使用 `setx`：

```powershell
setx ANTHROPIC_API_KEY "你的_API_Key"
setx ANTHROPIC_BASE_URL "你的_Base_URL"
```

`setx` 后需要重新打开终端，旧窗口不会自动更新。

> 注意：不要把 API Key 写进公开仓库，不要写进会提交的 `.env`、`.claude/settings.json`、README、截图或聊天记录。企业环境建议使用公司认可的密钥管理方式。

### 常见变量说明

| 变量 | 含义 | 常见用途 | 注意 |
| --- | --- | --- | --- |
| `ANTHROPIC_API_KEY` | API 密钥 | 直连 Anthropic API，或部分兼容接口按 `X-Api-Key` 使用 | 真实密钥不要泄露 |
| `ANTHROPIC_BASE_URL` | 自定义接口地址 | 指向自定义 Anthropic Compatible 或网关地址 | URL 是否包含 `/v1`、`/anthropic` 以平台文档为准 |
| `ANTHROPIC_AUTH_TOKEN` | 自定义 Bearer Token | 通过 Bearer Token 鉴权的代理、网关或平台 | 会作为认证 Token 使用，不要泄露 |
| `ANTHROPIC_CUSTOM_HEADERS` | 自定义请求头 | 某些网关要求额外 Header | 格式和是否支持以官方文档或工具说明为准 |
| `ANTHROPIC_CUSTOM_MODEL_OPTION` | 自定义模型选项 | 某些工具或网关用于传递模型选项 | 不是所有版本都支持，以官方文档或 CC Switch 说明为准 |
| `ENABLE_TOOL_SEARCH` | 开启工具搜索相关能力 | 非官方 Base URL 或部分第三方 Provider 下可能需要开启工具搜索 | 是否需要以 CC Switch、Claude Code 和 Provider 文档为准 |
| `CLAUDE_CODE_GIT_BASH_PATH` | 指定 Git Bash 路径 | Claude Code 找不到 Git Bash 时手动指定 | JSON 配置里路径要注意双反斜杠 |

### 删除或清空环境变量

PowerShell 当前窗口临时清空：

```powershell
Remove-Item Env:\ANTHROPIC_API_KEY
Remove-Item Env:\ANTHROPIC_BASE_URL
```

CMD 当前窗口临时清空：

```cmd
set ANTHROPIC_API_KEY=
set ANTHROPIC_BASE_URL=
```

永久变量如果要删除，可以在 Windows 系统设置中操作：

```text
设置 → 系统 → 关于 → 高级系统设置 → 环境变量
```

也可以使用 PowerShell 修改用户环境变量：

```powershell
[Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", $null, "User")
[Environment]::SetEnvironmentVariable("ANTHROPIC_BASE_URL", $null, "User")
```

执行后重新打开终端。

## CC Switch / ccswitch 安装

官方网站：

[https://ccswitch.io/](https://ccswitch.io/)

GitHub：

[https://github.com/farion1231/cc-switch](https://github.com/farion1231/cc-switch)

Releases：

[https://github.com/farion1231/cc-switch/releases](https://github.com/farion1231/cc-switch/releases)

### 安装建议

1. 优先从官网或 GitHub Releases 下载。
2. 不要从不明网盘、陌生群文件、广告弹窗、盗版下载站下载。
3. 官方 GitHub 仓库标题说明官方站点是 `ccswitch.io`。下载前确认域名和仓库地址。
4. 官方 GitHub 提醒：任何要求付款、充值、登录凭据的假冒 CC Switch 都要警惕。CC Switch 本身是配置管理工具，不应该索要你的模型平台登录密码。
5. 下载 Windows 安装包后正常安装。
6. 安装完成后打开 CC Switch。

> 注意：CC Switch GitHub README 可能会列出赞助商或第三方服务信息。本文不推荐、不背书任何不明来源的低价中转站。企业或客户环境应优先使用官方平台、自建网关或经过合规审核的服务。

### Windows 下载文件

在 Releases 页面中，通常选择类似名称的 Windows 安装包：

```text
CC-Switch-v{version}-Windows.msi
```

或便携版：

```text
CC-Switch-v{version}-Windows-Portable.zip
```

实际文件名会随版本变化，以 GitHub Releases 页面为准。

## CC Switch 配置模型

添加 Provider 时通常需要这些参数：

| 参数 | 含义 |
| --- | --- |
| Provider Name | 配置名称，比如 DeepSeek |
| API Key | 模型平台密钥 |
| Base URL | 接口地址 |
| Model Name | 模型名称 |
| Target App | 目标工具，例如 Claude Code |
| Enable / Apply | 启用配置 |

### 通用流程

1. 打开 CC Switch。
2. 新增 Provider。
3. 选择预设 Provider，或手动填写接口类型。
4. 填写 API Key。
5. 填写 Base URL。
6. 填写 Model Name。
7. 选择目标工具 Claude Code。
8. 点击 Apply / Switch / Enable。
9. 关闭并重启 Claude Code。
10. 测试是否生效。

> 注意：CC Switch 的按钮名称、界面布局、支持的 Provider Preset 会随版本更新。看不懂或找不到按钮时，以 CC Switch 官方网站、GitHub 仓库和内置说明为准。

## DeepSeek 示例

官网：

[https://platform.deepseek.com/](https://platform.deepseek.com/)

API 文档：

[https://api-docs.deepseek.com/](https://api-docs.deepseek.com/)

示例配置：

```text
Provider Name: DeepSeek
API Key: 你的_API_Key
Base URL: https://api.deepseek.com
Model Name: 以 DeepSeek 官方文档当前模型名为准
Target App: Claude Code
```

如果使用 Anthropic Format，则 Base URL 可能类似：

```text
https://api.deepseek.com/anthropic
```

> 注意：模型名会更新，必须以 DeepSeek 官方 Models & Pricing 或 API 文档为准。不要把旧教程里的模型名当成永久正确。先用最小测试确认可用，再放到日常项目里使用。

## Qwen / 阿里云百炼示例

百炼控制台：

[https://bailian.console.aliyun.com/](https://bailian.console.aliyun.com/)

DashScope 文档：

[https://help.aliyun.com/zh/model-studio/](https://help.aliyun.com/zh/model-studio/)

示例配置：

```text
Provider Name: Qwen
API Key: 你的_API_Key
Base URL: 以 DashScope OpenAI Compatible 官方文档为准
Model Name: qwen-plus / qwen-max / qwen-coder 等，以官方文档为准
Target App: Claude Code
```

注意事项：

| 项目 | 说明 |
| --- | --- |
| 地域 | DashScope 可能存在不同地域和不同接口地址 |
| 接口格式 | 不同模型可能支持不同调用方式 |
| 模型名 | `qwen-plus`、`qwen-max`、`qwen-coder` 等名称可能变化 |
| Base URL | 是否使用 OpenAI Compatible 地址，以官方文档为准 |

> 注意：Qwen / DashScope 的具体 Base URL、模型名、鉴权方式必须以阿里云官方文档为准。

## GLM / Kimi / SiliconFlow / OpenRouter 示例

### GLM / 智谱 AI

官网：

[https://open.bigmodel.cn/](https://open.bigmodel.cn/)

配置流程：

1. 注册或登录智谱 AI 开放平台。
2. 创建 API Key。
3. 查看官方文档中的 Base URL。
4. 查看当前可用模型名。
5. 填入 CC Switch Provider。
6. 切换后重启 Claude Code 测试。

示例：

```text
Provider Name: GLM
API Key: 你的_API_Key
Base URL: 以智谱 AI 官方文档为准
Model Name: 以智谱 AI 官方文档为准
Target App: Claude Code
```

### Kimi / 月之暗面

官网：

[https://platform.moonshot.cn/](https://platform.moonshot.cn/)

配置流程：

1. 注册或登录 Kimi 开放平台。
2. 创建 API Key。
3. 查看官方文档中的 Base URL。
4. 查看当前可用模型名。
5. 填入 CC Switch Provider。
6. 切换后重启 Claude Code 测试。

示例：

```text
Provider Name: Kimi
API Key: 你的_API_Key
Base URL: 以 Kimi 官方文档为准
Model Name: 以 Kimi 官方文档为准
Target App: Claude Code
```

### SiliconFlow / 硅基流动

官网：

[https://siliconflow.cn/](https://siliconflow.cn/)

配置流程：

1. 注册或登录 SiliconFlow。
2. 创建 API Key。
3. 查看官方文档中的 Base URL。
4. 查看平台支持的国产或开源模型名。
5. 填入 CC Switch Provider。
6. 切换后重启 Claude Code 测试。

示例：

```text
Provider Name: SiliconFlow
API Key: 你的_API_Key
Base URL: 以 SiliconFlow 官方文档为准
Model Name: 以 SiliconFlow 官方文档为准
Target App: Claude Code
```

### OpenRouter

官网：

[https://openrouter.ai/](https://openrouter.ai/)

配置流程：

1. 注册或登录 OpenRouter。
2. 创建 API Key。
3. 查看 OpenRouter 当前 Base URL 和模型名。
4. 选择需要的模型。
5. 填入 CC Switch Provider。
6. 切换后重启 Claude Code 测试。

示例：

```text
Provider Name: OpenRouter
API Key: 你的_API_Key
Base URL: 以 OpenRouter 官方文档为准
Model Name: 以 OpenRouter 官方模型列表为准
Target App: Claude Code
```

> 注意：OpenRouter 是多模型聚合接口，模型名和计费规则会变化。使用前先确认价格、上下文长度、工具调用兼容性和速率限制。

## New API / One API 自建网关说明

New API：

[https://github.com/Calcium-Ion/new-api](https://github.com/Calcium-Ion/new-api)

One API：

[https://github.com/songquanpeng/one-api](https://github.com/songquanpeng/one-api)

这类项目通常用于自建或公司内部统一 OpenAI Compatible API 网关。它们适合有运维能力、合规要求或统一计费需求的团队。

配置时通常需要：

| 项目 | 说明 |
| --- | --- |
| 网关地址 | 由你自己或团队部署得到 |
| API Key / Token | 网关生成或分发 |
| 上游渠道 | DeepSeek、Qwen、GLM、Kimi、OpenRouter、Anthropic 等 |
| 模型映射 | 网关里配置的模型名称可能和上游不同 |
| 鉴权方式 | 以网关项目文档和团队部署规范为准 |

> 注意：不要使用陌生人给你的 New API / One API 入口来输入密钥或账号。自建网关请做好 HTTPS、访问控制、日志脱敏、密钥轮换和权限隔离。

## 环境验证清单

### 1. 验证 Git

```powershell
git --version
```

正确现象：

```text
显示 git version x.x.x
```

### 2. 验证 Git Bash

```powershell
"C:\Program Files\Git\bin\bash.exe" --version
```

正确现象：

```text
显示 GNU bash 版本信息
```

### 3. 验证 Claude Code

```powershell
claude --version
```

正确现象：

```text
显示 Claude Code 版本号
```

### 4. 验证 Claude 能启动

```powershell
claude
```

正确现象：

```text
进入 Claude Code 交互界面
```

### 5. 验证登录状态

在 Claude Code 中输入：

```text
/login
```

正确现象：

```text
能完成登录或显示已登录
```

### 6. 验证项目读写

在项目目录运行：

```powershell
claude
```

然后输入：

```text
请创建 test.md，写入“Claude Code 环境测试成功”。
```

退出后检查：

```cmd
dir
```

正确现象：

```text
目录里出现 test.md
```

### 7. 验证命令执行

在 Claude Code 中输入：

```text
请运行 dir，并解释当前目录文件。
```

正确现象：

```text
Claude 能调用命令并返回目录内容。
```

### 8. 验证模型切换

在 CC Switch 切换 Provider 后：

1. 关闭 Claude Code。
2. 重新打开终端。
3. 进入项目目录。
4. 运行 `claude`。
5. 输入：

```text
请用一句话说明当前模型接口是否响应正常。
```

正确现象：

```text
模型能正常回复，无 API Key / Base URL / model not found 报错。
```

### 9. 验证 API Key 是否有效

如果是 OpenAI Compatible 接口，可以用 `curl` 做最小测试。但不同平台格式不同，所以请求路径、请求体、模型名、Header 都需要以平台官方文档为准。

PowerShell 示例：

```powershell
$env:TEST_API_KEY="你的_API_Key"
curl.exe "https://你的_Base_URL/chat/completions" `
  -H "Authorization: Bearer $env:TEST_API_KEY" `
  -H "Content-Type: application/json" `
  -d "{\"model\":\"你的模型名\",\"messages\":[{\"role\":\"user\",\"content\":\"ping\"}]}"
```

CMD 示例：

```cmd
set TEST_API_KEY=你的_API_Key
curl "https://你的_Base_URL/chat/completions" -H "Authorization: Bearer %TEST_API_KEY%" -H "Content-Type: application/json" -d "{\"model\":\"你的模型名\",\"messages\":[{\"role\":\"user\",\"content\":\"ping\"}]}"
```

Git Bash 示例：

```bash
export TEST_API_KEY="你的_API_Key"
curl "https://你的_Base_URL/chat/completions" \
  -H "Authorization: Bearer $TEST_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"你的模型名","messages":[{"role":"user","content":"ping"}]}'
```

常见状态码：

| 状态码 | 常见含义 |
| --- | --- |
| 401 | API Key 错误 |
| 403 | 无权限、余额不足或账号未开通 |
| 404 | Base URL、路径或模型名错误 |
| 429 | 频率限制、额度耗尽或余额不足 |
| 500 | 平台服务异常或网关问题 |

> 注意：有些平台 Base URL 已经包含 `/v1`，有些没有；有些平台是 `/chat/completions`，有些是 Anthropic Messages 格式。不要盲目拼接路径，以官方文档为准。

## 一键自检命令清单

> 注意：下面命令会显示环境变量值。如果变量中有真实 API Key，不要截图或分享输出结果。

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

## 常见问题 FAQ

### 1. `claude` 不是内部或外部命令

| 项目 | 说明 |
| --- | --- |
| 现象 | 输入 `claude --version` 后提示不是内部或外部命令，也不是可运行程序。 |
| 原因 | Claude Code 没安装成功，或 PATH 没刷新，或终端仍是安装前打开的旧窗口。 |
| 解决方法 | 关闭终端重新打开；运行安装命令；重启电脑；检查安装目录是否加入 PATH；以官方安装排错文档为准。 |

### 2. `irm` 不识别

| 项目 | 说明 |
| --- | --- |
| 现象 | 输入 `irm https://claude.ai/install.ps1 \| iex` 后提示 `irm` 不存在。 |
| 原因 | 你在 CMD 里运行了 PowerShell 命令。 |
| 解决方法 | 打开 PowerShell 运行 `irm` 命令，或在 CMD 中使用官方 CMD 安装命令。 |

### 3. `&&` 报错

| 项目 | 说明 |
| --- | --- |
| 现象 | 输入 CMD 安装命令后，提示 `&&` 不是有效语句分隔符。 |
| 原因 | 你可能在 PowerShell 中运行了 CMD 命令。 |
| 解决方法 | 打开 CMD 后运行 CMD 安装命令；或在 PowerShell 使用 `irm https://claude.ai/install.ps1 \| iex`。 |

### 4. Git Bash 找不到

| 项目 | 说明 |
| --- | --- |
| 现象 | Claude Code 提示找不到 Bash，或命令执行行为和预期不同。 |
| 原因 | 没安装 Git for Windows，或 Git Bash 路径不在默认位置。 |
| 解决方法 | 安装 Git for Windows；验证 `"C:\Program Files\Git\bin\bash.exe" --version`；必要时配置 `CLAUDE_CODE_GIT_BASH_PATH`，以官方文档为准。 |

### 5. API Key 无效

| 项目 | 说明 |
| --- | --- |
| 现象 | 返回 401、unauthorized、invalid api key。 |
| 原因 | API Key 复制错误、过期、被删除、平台不匹配、Header 类型不对。 |
| 解决方法 | 重新创建 API Key；确认没有多余空格；确认平台要求使用 `X-Api-Key` 还是 `Authorization: Bearer`；以平台文档为准。 |

### 6. Base URL 填错

| 项目 | 说明 |
| --- | --- |
| 现象 | 返回 404、502、连接失败或一直无响应。 |
| 原因 | Base URL 少了或多了 `/v1`、路径写错、把网页地址当成 API 地址、网络代理问题。 |
| 解决方法 | 回到平台 API 文档复制 Base URL；确认 CC Switch 里是否自动拼接路径；用最小 `curl` 测试。 |

### 7. 模型名错误

| 项目 | 说明 |
| --- | --- |
| 现象 | 返回 `model not found`、`invalid model`、模型不可用。 |
| 原因 | 模型名过期、拼写错误、账号无权限、网关里模型映射名不同。 |
| 解决方法 | 查看平台当前 Models 文档；在 CC Switch 中更新 Model Name；如果使用 New API / One API，检查网关模型映射。 |

### 8. 切换模型后没有变化

| 项目 | 说明 |
| --- | --- |
| 现象 | CC Switch 切换了 Provider，但 Claude Code 仍像原来的模型或账号。 |
| 原因 | Claude Code 会话没重启、终端环境变量没刷新、官方登录凭据和自定义 API 配置同时存在、Provider 没有 Apply。 |
| 解决方法 | 关闭 Claude Code；重新打开终端；确认 CC Switch 当前 Provider；检查 `ANTHROPIC_API_KEY`、`ANTHROPIC_BASE_URL`；必要时 `/logout` 后重新登录。 |

### 9. 国产模型能聊天但不能正常写代码

| 项目 | 说明 |
| --- | --- |
| 现象 | 普通问答正常，但改文件、工具调用、长任务、JSON 输出经常失败。 |
| 原因 | 模型对工具调用、函数调用、长上下文、流式输出或 Anthropic Format 的兼容性不足。 |
| 解决方法 | 换更适合代码的模型；查看 CC Switch 是否有专门 Provider Preset；缩小任务范围；先做小文件测试；以平台兼容说明为准。 |

### 10. Claude Code 工具调用异常

| 项目 | 说明 |
| --- | --- |
| 现象 | Claude 不能运行命令、不能读写文件、工具调用返回格式错误。 |
| 原因 | 权限策略限制、终端 Shell 异常、第三方 Provider 不完全兼容工具调用。 |
| 解决方法 | 检查 Claude Code 权限提示；先用官方 Claude 登录测试；再切换第三方 Provider 对比；必要时开启或检查 `ENABLE_TOOL_SEARCH`，以官方文档和 CC Switch 说明为准。 |

### 11. 权限弹窗很多

| 项目 | 说明 |
| --- | --- |
| 现象 | Claude Code 每次读写文件或运行命令都询问权限。 |
| 原因 | Claude Code 的权限保护机制在工作，或当前项目还没有信任配置。 |
| 解决方法 | 仔细阅读权限提示；只允许你理解的命令；可在 Claude Code 配置中调整权限策略，具体以官方权限文档为准。 |

### 12. 中文路径导致问题

| 项目 | 说明 |
| --- | --- |
| 现象 | 命令找不到文件、脚本乱码、依赖安装失败、工具路径解析错误。 |
| 原因 | 某些 CLI 工具、脚本或依赖对中文路径、空格、特殊字符兼容不好。 |
| 解决方法 | 把项目放到 `C:\AI-Tools\Projects\demo` 这类简单英文路径下；避免桌面、下载目录和带特殊符号的路径。 |

### 13. `setx` 后变量没生效

| 项目 | 说明 |
| --- | --- |
| 现象 | `setx` 显示成功，但 `echo $env:ANTHROPIC_API_KEY` 看不到新值。 |
| 原因 | `setx` 修改的是新终端会读取的用户环境变量，当前旧窗口不会自动更新。 |
| 解决方法 | 关闭并重新打开终端；必要时重启电脑；检查是否设置到了用户变量而非系统变量。 |

### 14. CC Switch 下载到假网站

| 项目 | 说明 |
| --- | --- |
| 现象 | 下载站要求输入登录密码、充值、付款、安装奇怪插件或提供网盘链接。 |
| 原因 | 可能访问了假冒网站、广告站或二次打包安装包。 |
| 解决方法 | 只从 `https://ccswitch.io/` 或 `https://github.com/farion1231/cc-switch/releases` 下载；不要输入模型平台密码；可删除可疑安装包并重新从官方来源下载。 |

### 15. 模型响应慢或失败

| 项目 | 说明 |
| --- | --- |
| 现象 | Claude Code 回复很慢、超时、频繁 429/500。 |
| 原因 | 平台限流、余额不足、网络代理不稳定、模型繁忙、网关异常、请求上下文过长。 |
| 解决方法 | 检查平台状态和余额；换网络或代理；缩短上下文；换模型；稍后重试；如果使用中转或自建网关，检查网关日志。 |

## 最简安装流程

1. 安装 Git for Windows。
2. 安装 Claude Code。
3. 运行 `claude --version`。
4. 创建项目目录。
5. 运行 `claude`。
6. 登录 Claude。
7. 安装 CC Switch。
8. 在 CC Switch 添加 DeepSeek / Qwen Provider。
9. Apply / Switch。
10. 重启 Claude Code。
11. 测试读写文件。
12. 测试运行命令。
13. 测试模型回复。

## 交付给客户前的最终检查

| 检查项 | 是否完成 |
| --- | --- |
| 文件是否存在 | 是，目标文件为 `docs/zh/windows/setup.md` |
| 一级标题是否正确 | 是 |
| 是否包含网站清单 | 是 |
| 是否包含命令清单 | 是 |
| 是否包含环境验证 | 是 |
| 是否包含 FAQ | 是 |
| Markdown 代码块是否闭合 | 是，建议提交前再用 Markdown 预览确认 |
