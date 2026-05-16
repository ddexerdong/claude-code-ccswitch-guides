# macOS 系统配置 Claude Code，并使用 CC Switch 切换国产模型完整教程

> 注意：本文只提供 macOS 安装与配置说明，不会替你执行任何安装命令。涉及 Claude Code、CC Switch、模型平台 API、Base URL、模型名称时，均以官方文档为准。

## 参考网站

只需要注册你实际使用的平台，不需要把所有模型平台都注册一遍。

| 网站 | 用途 |
| --- | --- |
| [Claude Code 官方文档](https://code.claude.com/docs/) | 查看 Claude Code 功能、安装、配置、权限和常见问题。 |
| [Claude Code Quickstart](https://code.claude.com/docs/en/quickstart) | 查看 `claude` 命令、登录、项目启动和基础使用。 |
| [Claude Code Setup](https://code.claude.com/docs/en/setup) | 查看 macOS 安装方式、系统要求和更新说明。 |
| [Claude Code Environment Variables](https://code.claude.com/docs/en/env-vars) | 查看 `ANTHROPIC_API_KEY`、`ANTHROPIC_BASE_URL` 等变量。 |
| [Claude Code Settings](https://code.claude.com/docs/en/settings) | 查看 `settings.json`、`/config`、用户配置和项目配置。 |
| [Anthropic Console](https://console.anthropic.com/) | 申请或管理 Anthropic API Key。 |
| [CC Switch 官网](https://ccswitch.io/) | 下载和了解 CC Switch。 |
| [CC Switch GitHub](https://github.com/farion1231/cc-switch) | 查看源码、说明、更新记录和安全提醒。 |
| [CC Switch Releases](https://github.com/farion1231/cc-switch/releases) | 手动下载 macOS 安装包。 |
| [Homebrew](https://brew.sh/) | 安装和管理 macOS 开发工具。 |
| [Git](https://git-scm.com/) | 下载 Git、查看 Git 文档。 |
| [VS Code](https://code.visualstudio.com/) | 代码编辑器和项目管理工具。 |
| [Python](https://www.python.org/downloads/macos/) | Python macOS 安装包和文档。 |
| [Node.js](https://nodejs.org/) | Node.js LTS 下载和文档。 |
| [DeepSeek Platform](https://platform.deepseek.com/) | 申请 DeepSeek API Key，查看余额。 |
| [DeepSeek API Docs](https://api-docs.deepseek.com/) | 查看 DeepSeek Base URL、模型名和 API 格式。 |
| [阿里云百炼 / DashScope](https://bailian.console.aliyun.com/) | 管理 Qwen / 通义千问 API Key、模型和用量。 |
| [DashScope 文档](https://help.aliyun.com/zh/model-studio/) | 查看 Qwen OpenAI Compatible 接口、模型名和调用方式。 |
| [智谱 AI](https://open.bigmodel.cn/) | 管理 GLM API Key 和模型。 |
| [Kimi / Moonshot](https://platform.moonshot.cn/) | 管理 Kimi API Key 和模型。 |
| [SiliconFlow](https://siliconflow.cn/) | 管理国产和开源模型 API Key。 |
| [OpenRouter](https://openrouter.ai/) | 使用多模型聚合接口。 |
| [New API](https://github.com/Calcium-Ion/new-api) | 自建或使用 OpenAI Compatible API 网关。 |
| [One API](https://github.com/songquanpeng/one-api) | 自建或使用 OpenAI Compatible API 网关。 |

> 注意：CC Switch 只建议从官网或 GitHub Releases 下载。不要从网盘、私信链接、广告下载站或不明来源安装包下载工具。

## 1. 适用对象

本文适用于：

- macOS 用户。
- 需要安装 Claude Code。
- 需要使用 CC Switch 切换 DeepSeek / Qwen / GLM / Kimi 等模型。
- 需要搭建 AI 编程工作流。

三者关系：

| 工具 | 普通理解 |
| --- | --- |
| Claude Code | AI 编程工作台，可以读项目、改代码、运行命令 |
| DeepSeek / Qwen / GLM / Kimi | AI 大脑，负责模型推理 |
| CC Switch | 模型切换器，管理 API Key、Base URL 和模型名 |

## 2. 安装前准备

| 环境 | 是否必须 | 作用 |
| --- | --- | --- |
| macOS | 必须 | 系统环境 |
| Terminal / iTerm2 | 必须 | 执行命令 |
| Homebrew | 推荐必须 | 安装 Git、Node、Python、CC Switch 等工具 |
| Git | 推荐必须 | 项目版本管理 |
| Claude Code | 必须 | AI 编程助手 |
| CC Switch | 可选但推荐 | 管理和切换模型 |
| VS Code | 推荐 | 编辑项目 |
| Python 3.10+ | 推荐 | 自动化脚本 |
| Node.js LTS | 推荐 | 部分 CLI 工具 |
| API Key | 如果接国产模型则必须 | 调用模型接口 |

## 3. 推荐目录结构

建议建立：

```text
~/AI-Tools/
├── ClaudeCode/
├── CC-Switch/
├── Projects/
├── Docs/
└── Backup/
```

建议：

| 建议 | 原因 |
| --- | --- |
| 不建议放在桌面 | 桌面容易被 iCloud 同步，路径和权限容易混乱 |
| 不建议中文路径 | 部分 CLI 工具对中文路径兼容不好 |
| 不建议路径包含特殊符号 | 空格、括号、`#`、`&` 可能导致脚本解析问题 |
| 推荐英文路径 | 便于复制命令和团队排查 |

## 4. 安装 Homebrew

官网：

[https://brew.sh/](https://brew.sh/)

在 Terminal 中运行：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

验证：

```bash
brew --version
```

Apple Silicon Mac 可能需要把 Homebrew 加入 PATH：

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

常见路径：

| Mac 类型 | Homebrew 常见路径 |
| --- | --- |
| Intel Mac | `/usr/local/bin/brew` |
| Apple Silicon Mac | `/opt/homebrew/bin/brew` |

> 注意：如果 `brew --version` 报 `command not found`，先确认 Homebrew 安装是否完成，再检查 PATH。

## 5. 安装 Git

```bash
brew install git
```

验证：

```bash
git --version
```

## 6. 安装 Node.js

```bash
brew install node
```

验证：

```bash
node --version
npm --version
```

说明：如果 Claude Code 官方安装方式不要求 Node.js，也建议安装 Node.js LTS 作为通用开发环境。具体依赖以官方文档为准。

## 7. 安装 Python

```bash
brew install python
```

验证：

```bash
python3 --version
pip3 --version
```

## 8. 安装 Claude Code

安装方式必须以 Claude Code 官方文档为准：

- [Claude Code Setup](https://code.claude.com/docs/en/setup)
- [Claude Code Quickstart](https://code.claude.com/docs/en/quickstart)

常用思路：

1. 打开官方 Setup 文档。
2. 选择官方推荐的 macOS 安装方式。
3. 完成安装后重新打开 Terminal。
4. 验证命令是否可用。

验证：

```bash
claude --version
```

启动：

```bash
claude
```

登录：

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

> 注意：如果 `claude` 命令不存在，先重启 Terminal，再检查安装步骤和 PATH。仍不行时，以官方安装排错文档为准。

## 9. 安装 CC Switch

### 方式一：Homebrew 安装

```bash
brew tap farion1231/ccswitch
brew install --cask cc-switch
```

更新：

```bash
brew upgrade --cask cc-switch
```

### 方式二：GitHub Releases 手动下载

访问：

[https://github.com/farion1231/cc-switch/releases](https://github.com/farion1231/cc-switch/releases)

下载：

```text
CC-Switch-v{version}-macOS.dmg
```

或：

```text
CC-Switch-v{version}-macOS.zip
```

说明：

- 优先从官网或 GitHub Releases 下载。
- 不要从不明网盘下载。
- macOS 可能会提示安全验证。
- 如果打不开，到系统设置的“隐私与安全”里允许打开。

> 注意：任何要求你向 CC Switch 输入模型平台登录密码、付款、充值、转账的页面都要警惕。CC Switch 是配置管理工具，不应索要你的平台登录凭据。

## 10. 配置环境变量

macOS 默认 Shell 通常是 `zsh`，常见配置文件：

```text
~/.zshrc
~/.zprofile
```

临时设置：

```bash
export ANTHROPIC_API_KEY="你的_API_Key"
export ANTHROPIC_BASE_URL="你的_Base_URL"
```

永久写入：

```bash
echo 'export ANTHROPIC_API_KEY="你的_API_Key"' >> ~/.zshrc
echo 'export ANTHROPIC_BASE_URL="你的_Base_URL"' >> ~/.zshrc
source ~/.zshrc
```

查看：

```bash
echo $ANTHROPIC_API_KEY
echo $ANTHROPIC_BASE_URL
```

> 注意：不要把 API Key 发给别人，不要截图暴露 API Key，不要写入公开 GitHub 仓库。如果泄露，立即去平台删除旧 Key 并创建新 Key。

常见变量：

| 变量 | 用途 |
| --- | --- |
| `ANTHROPIC_API_KEY` | API 密钥 |
| `ANTHROPIC_BASE_URL` | 自定义模型接口地址 |
| `ANTHROPIC_AUTH_TOKEN` | Bearer Token，具体以官方文档为准 |
| `ANTHROPIC_CUSTOM_HEADERS` | 自定义请求头，具体以官方文档为准 |

## 11. 使用 CC Switch 配置模型

添加 Provider 通常需要：

| 参数 | 含义 |
| --- | --- |
| Provider Name | 配置名称 |
| API Key | 模型平台密钥 |
| Base URL | 模型接口地址 |
| Model Name | 模型名称 |
| Target App | 目标应用，例如 Claude Code |

流程：

1. 打开 CC Switch。
2. 新建 Provider。
3. 填 API Key。
4. 填 Base URL。
5. 填 Model Name。
6. 选择 Claude Code。
7. Apply / Switch。
8. 重启 Claude Code。
9. 测试。

## 12. DeepSeek 示例配置

官网：

[https://platform.deepseek.com/](https://platform.deepseek.com/)

API 文档：

[https://api-docs.deepseek.com/](https://api-docs.deepseek.com/)

示例：

```text
Provider Name: DeepSeek
API Key: 你的_API_Key
Base URL: 以 DeepSeek 官方文档为准
Model Name: 以 DeepSeek 官方文档为准
Target App: Claude Code
```

> 注意：模型名和接口可能变化，必须以 DeepSeek 官方文档为准。不要把旧教程里的模型名当成永久正确。

## 13. Qwen / GLM / Kimi / SiliconFlow / OpenRouter 示例配置

| Provider | 官网 | API Key 获取位置 | Base URL 查看位置 | Model Name 查看位置 |
| --- | --- | --- | --- | --- |
| Qwen / DashScope | [阿里云百炼](https://bailian.console.aliyun.com/) | 百炼控制台 | [DashScope 文档](https://help.aliyun.com/zh/model-studio/) | DashScope 模型文档 |
| GLM | [智谱 AI](https://open.bigmodel.cn/) | 智谱开放平台 | 智谱官方文档 | 智谱模型列表 |
| Kimi | [Moonshot](https://platform.moonshot.cn/) | Kimi 开放平台 | Kimi 官方文档 | Kimi 模型列表 |
| SiliconFlow | [SiliconFlow](https://siliconflow.cn/) | SiliconFlow 控制台 | SiliconFlow 官方文档 | SiliconFlow 模型列表 |
| OpenRouter | [OpenRouter](https://openrouter.ai/) | OpenRouter 控制台 | OpenRouter 文档 | OpenRouter 模型列表 |

通用步骤：

1. 注册并登录对应平台。
2. 创建 API Key。
3. 查看官方 Base URL。
4. 查看官方 Model Name。
5. 填入 CC Switch。
6. Apply / Switch。
7. 重启 Claude Code 测试。

> 注意：不同平台的 OpenAI Compatible / Anthropic Compatible 接口可能不同，具体以官方文档为准。

## 14. 如何验证环境正确

### 验证 Homebrew

```bash
brew --version
```

### 验证 Git

```bash
git --version
```

### 验证 Node

```bash
node --version
npm --version
```

### 验证 Python

```bash
python3 --version
pip3 --version
```

### 验证 Claude Code

```bash
claude --version
claude
```

### 验证环境变量

```bash
echo $ANTHROPIC_API_KEY
echo $ANTHROPIC_BASE_URL
```

### 验证项目读写

```bash
mkdir -p ~/AI-Tools/Projects/demo
cd ~/AI-Tools/Projects/demo
claude
```

进入 Claude 后输入：

```text
请创建 test.md，内容为“Claude Code macOS 环境测试成功”。
```

退出后检查：

```bash
ls
```

正确现象：目录中出现 `test.md`。

## 15. 常见问题 FAQ

### 1. `brew: command not found`

| 项目 | 说明 |
| --- | --- |
| 现象 | 输入 `brew --version` 后提示找不到命令。 |
| 原因 | Homebrew 未安装，或 PATH 没配置。 |
| 解决方法 | 按官网安装 Homebrew；Apple Silicon Mac 检查 `/opt/homebrew/bin/brew` 是否加入 PATH。 |

### 2. `claude: command not found`

| 项目 | 说明 |
| --- | --- |
| 现象 | 输入 `claude --version` 后提示找不到命令。 |
| 原因 | Claude Code 未安装成功，或终端 PATH 未刷新。 |
| 解决方法 | 重新打开 Terminal；检查官方安装步骤；仍失败时以官方文档为准。 |

### 3. `.zshrc` 修改后不生效

| 项目 | 说明 |
| --- | --- |
| 现象 | 已写入环境变量，但 `echo` 看不到。 |
| 原因 | 没有执行 `source ~/.zshrc`，或写入了错误配置文件。 |
| 解决方法 | 执行 `source ~/.zshrc`；新开 Terminal；检查默认 Shell。 |

### 4. API Key 无效

| 项目 | 说明 |
| --- | --- |
| 现象 | 报 401、invalid api key、unauthorized。 |
| 原因 | Key 错误、过期、平台不匹配或复制了空格。 |
| 解决方法 | 到平台官网重新生成 Key；替换 CC Switch 配置；重启 Claude Code。 |

### 5. Base URL 错误

| 项目 | 说明 |
| --- | --- |
| 现象 | 报 404、连接失败、网关错误。 |
| 原因 | Base URL 拼错，或 `/v1`、`/anthropic` 路径不符合平台要求。 |
| 解决方法 | 回到平台官方 API 文档复制地址，以官方文档为准。 |

### 6. `model not found`

| 项目 | 说明 |
| --- | --- |
| 现象 | 模型不存在或不可用。 |
| 原因 | 模型名过期、拼写错误或账号无权限。 |
| 解决方法 | 查看平台当前模型列表，在 CC Switch 中更新 Model Name。 |

### 7. CC Switch 切换后没变化

| 项目 | 说明 |
| --- | --- |
| 现象 | 切换 Provider 后 Claude Code 仍像旧模型。 |
| 原因 | 没有 Apply / Switch，或 Claude Code 没重启，或环境变量被旧配置覆盖。 |
| 解决方法 | Apply 后关闭 Claude Code，重新打开 Terminal 再启动。 |

### 8. macOS 阻止打开应用

| 项目 | 说明 |
| --- | --- |
| 现象 | 双击 CC Switch 后提示无法打开。 |
| 原因 | macOS Gatekeeper 安全校验。 |
| 解决方法 | 确认来自官网或 GitHub Releases；到系统设置的“隐私与安全”允许打开。 |

### 9. 权限不足

| 项目 | 说明 |
| --- | --- |
| 现象 | 无法写文件、无法访问目录。 |
| 原因 | 当前目录权限不足，或 macOS 隐私权限限制。 |
| 解决方法 | 把项目放到 `~/AI-Tools/Projects/`；必要时检查系统设置中的文件访问权限。 |

### 10. 中文路径或空格路径导致问题

| 项目 | 说明 |
| --- | --- |
| 现象 | 命令找不到文件、脚本报错。 |
| 原因 | 路径编码或空格转义问题。 |
| 解决方法 | 使用简单英文路径，例如 `~/AI-Tools/Projects/demo`。 |

### 11. 模型能聊天但不能正常工具调用

| 项目 | 说明 |
| --- | --- |
| 现象 | 普通问答正常，但改文件、运行命令、工具调用失败。 |
| 原因 | 第三方模型或接口不完全兼容 Claude Code 工具调用。 |
| 解决方法 | 换更适合 coding 的模型；使用平台推荐接口；必要时切回官方 Claude 模型对比。 |

### 12. 网络连接失败

| 项目 | 说明 |
| --- | --- |
| 现象 | 安装、登录、模型调用超时。 |
| 原因 | 网络不稳定、代理配置错误、平台服务异常。 |
| 解决方法 | 检查网络和代理；查看平台状态；稍后重试。 |

## 16. 最简安装流程

1. 安装 Homebrew。
2. 安装 Git。
3. 安装 Node.js 和 Python。
4. 按 Claude Code 官方文档安装 Claude Code。
5. 运行 `claude --version`。
6. 创建 `~/AI-Tools/Projects/demo`。
7. 运行 `claude` 并登录。
8. 安装 CC Switch。
9. 在 CC Switch 添加 DeepSeek / Qwen / GLM / Kimi Provider。
10. Apply / Switch 后重启 Claude Code，测试文件读写和模型回复。
