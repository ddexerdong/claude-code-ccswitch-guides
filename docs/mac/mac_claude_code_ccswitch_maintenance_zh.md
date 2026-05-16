# macOS Claude Code + CC Switch + 国产模型配置维护指南

> 注意：本文是维护指南，不会替你执行任何安装、更新、删除或重置命令。更新和配置变更前请确认来源可靠，并以官方文档为准。

## 维护时常用网站

| 网站 | 用途 |
| --- | --- |
| [Claude Code 官方文档](https://code.claude.com/docs/) | 查看安装、配置、权限、更新、环境变量和常见问题。 |
| [Claude Code Quickstart](https://code.claude.com/docs/en/quickstart) | 查看基础启动、登录和常用命令。 |
| [Claude Code Setup](https://code.claude.com/docs/en/setup) | 查看 macOS 安装、系统要求和更新说明。 |
| [Claude Code Environment Variables](https://code.claude.com/docs/en/env-vars) | 查看 `ANTHROPIC_API_KEY`、`ANTHROPIC_BASE_URL` 等变量。 |
| [Claude Code Settings](https://code.claude.com/docs/en/settings) | 查看 `settings.json`、用户配置和项目配置。 |
| [Anthropic Console](https://console.anthropic.com/) | 管理 Anthropic API Key。 |
| [CC Switch 官网](https://ccswitch.io/) | 下载和了解 CC Switch。 |
| [CC Switch GitHub](https://github.com/farion1231/cc-switch) | 查看说明、更新记录和安全提醒。 |
| [CC Switch Releases](https://github.com/farion1231/cc-switch/releases) | 手动下载最新版安装包。 |
| [Homebrew](https://brew.sh/) | 维护 macOS 开发工具。 |
| [Git](https://git-scm.com/) | 查看 Git 文档和下载入口。 |
| [VS Code](https://code.visualstudio.com/) | 编辑项目和文档。 |
| [Python](https://www.python.org/downloads/macos/) | Python macOS 下载和文档。 |
| [Node.js](https://nodejs.org/) | Node.js LTS 下载和文档。 |
| [DeepSeek Platform](https://platform.deepseek.com/) | 查看余额、API Key、模型状态。 |
| [DeepSeek API Docs](https://api-docs.deepseek.com/) | 查看 Base URL、模型名和 API 格式。 |
| [阿里云百炼 / DashScope](https://bailian.console.aliyun.com/) | 管理 Qwen API Key、模型和用量。 |
| [DashScope 文档](https://help.aliyun.com/zh/model-studio/) | 查看 OpenAI Compatible 接口、模型名和调用方式。 |
| [智谱 AI](https://open.bigmodel.cn/) | 管理 GLM API Key 和模型。 |
| [Kimi / Moonshot](https://platform.moonshot.cn/) | 管理 Kimi API Key 和模型。 |
| [SiliconFlow](https://siliconflow.cn/) | 管理国产和开源模型 API Key。 |
| [OpenRouter](https://openrouter.ai/) | 管理多模型聚合接口。 |
| [New API](https://github.com/Calcium-Ion/new-api) | 自建或使用 OpenAI Compatible API 网关。 |
| [One API](https://github.com/songquanpeng/one-api) | 自建或使用 OpenAI Compatible API 网关。 |

> 注意：只从官网或 GitHub Releases 下载 CC Switch。不要从不明网盘、私信链接、不明下载站获取安装包，也不要使用不明来源中转站。

## 1. 维护对象说明

这套环境通常包含：

| 对象 | 普通解释 | 维护重点 |
| --- | --- | --- |
| Claude Code | AI 编程工作台 | 能否启动、登录、读写项目、运行命令 |
| Homebrew | macOS 工具管理器 | `brew` 是否正常，软件是否可更新 |
| Git | 版本管理工具 | `git` 是否可用 |
| Node.js / Python | 常用开发运行环境 | 版本是否正常 |
| CC Switch | 模型配置和切换工具 | Provider 是否正确，切换是否生效 |
| API Key | 调用模型的密码 | 是否有效、是否泄露、是否过期 |
| Base URL | 模型接口地址 | 是否和官方文档一致 |
| Model Name | 具体模型名 | 是否仍可用 |
| 项目目录 | 工作文件夹 | 是否可读写、路径是否规范 |

## 2. 每次使用前快速检查

```bash
brew --version
git --version
node --version
python3 --version
claude --version
echo $ANTHROPIC_API_KEY
echo $ANTHROPIC_BASE_URL
```

正确现象：

| 检查项 | 正常表现 |
| --- | --- |
| Homebrew | 显示版本号 |
| Git | 显示 `git version x.x.x` |
| Node.js | 显示版本号 |
| Python | 显示 Python 3 版本号 |
| Claude Code | 显示 Claude Code 版本号 |
| API Key | 使用第三方模型时应已配置；官方登录时可为空 |
| Base URL | 使用第三方模型时应已配置；官方登录时可为空 |

> 注意：`echo $ANTHROPIC_API_KEY` 会显示密钥，不要截图或转发输出。

## 3. Claude Code 是否正常

检查：

```bash
claude --version
claude
```

进入 Claude Code 后输入：

```text
请创建 test.md，内容为“Claude Code macOS 环境测试成功”。
```

退出后检查：

```bash
ls
```

正常表现：

- 能进入 Claude Code。
- 能创建 `test.md`。
- 能读写当前项目文件。
- 能执行简单命令。

异常处理：

| 异常 | 处理 |
| --- | --- |
| `claude: command not found` | 重启 Terminal，检查安装和 PATH，以官方文档为准 |
| 无法登录 | 检查网络、浏览器跳转、账号权限 |
| 无法读写文件 | 换到 `~/AI-Tools/Projects/` 下测试 |
| 权限提示很多 | 仔细阅读权限提示，只允许理解且安全的操作 |

## 4. Homebrew 是否正常

检查：

```bash
brew --version
```

更新 Homebrew 索引：

```bash
brew update
```

升级已安装软件：

```bash
brew upgrade
```

> 注意：更新前先保存工作。企业电脑如有软件管控，请按公司规范操作。

常见问题：

| 现象 | 原因 | 解决方法 |
| --- | --- | --- |
| `brew: command not found` | 未安装或 PATH 不正确 | 按 Homebrew 官网修复 PATH |
| 更新很慢 | 网络或源问题 | 检查网络，必要时稍后重试 |
| 权限错误 | 安装目录权限异常 | 以 Homebrew 官方文档为准 |

## 5. Git 是否正常

```bash
git --version
```

如果 Git 不正常：

1. 确认 Homebrew 正常。
2. 确认 Git 已安装。
3. 重新打开 Terminal。
4. 必要时参考 Git 官方文档。

## 6. CC Switch 是否正常

检查内容：

| 检查项 | 要看什么 |
| --- | --- |
| 应用能否打开 | CC Switch 窗口能正常出现 |
| Provider 列表 | 能看到常用 Provider |
| 当前 Provider | 是否是目标模型平台 |
| API Key | 是否已填写且未过期 |
| Base URL | 是否来自官方文档 |
| Model Name | 是否仍可用 |
| Apply / Switch | 是否已点击 |
| Claude Code | 切换后是否重启 |

验证流程：

```bash
cd ~/AI-Tools/Projects/demo
claude
```

进入 Claude Code 后输入：

```text
请用一句话说明当前模型接口是否响应正常。
```

正确现象：模型能正常回复，没有 401、403、404、429、`model not found` 或 Base URL 错误。

## 7. API Key 如何更换

需要更换的情况：

- Key 泄露。
- Key 过期。
- 平台余额不足或换账号。
- 切换模型平台。
- 报 401 Unauthorized。
- 报 invalid api key。

更换流程：

1. 登录模型平台官网。
2. 删除或禁用旧 Key。
3. 创建新 Key。
4. 打开 CC Switch。
5. 替换 API Key。
6. Apply / Switch。
7. 重启 Claude Code。
8. 测试模型回复。

> 注意：不要把 API Key 明文写进文档、README、Git 仓库或截图。怀疑泄露时立即删除旧 Key。

## 8. Base URL 和模型名如何维护

维护原则：

| 项目 | 说明 |
| --- | --- |
| Base URL | 模型接口地址，一个字符错误也可能导致失败 |
| Model Name | 平台当前支持的模型名 |
| 官方文档 | 所有地址、路径、模型名以官方文档为准 |
| 旧教程 | 只能参考，不要当作永久正确 |

维护流程：

1. 打开模型官方文档。
2. 找到 Base URL。
3. 找到 Model Name。
4. 填入 CC Switch。
5. Apply / Switch。
6. 重启 Claude Code。
7. 测试。

## 9. 如何更新 Claude Code

原则：

- 优先查看 Claude Code 官方 Setup 文档。
- 使用官方推荐方式更新。
- 更新前保存工作并退出 Claude Code。
- 更新后检查版本。

检查：

```bash
claude --version
```

> 注意：Claude Code 更新方式可能变化，以官方文档为准。

## 10. 如何更新 CC Switch

如果使用 Homebrew 安装：

```bash
brew upgrade --cask cc-switch
```

如果手动安装：

1. 访问 [CC Switch Releases](https://github.com/farion1231/cc-switch/releases)。
2. 下载最新版 macOS 安装包。
3. 安装前备份 Provider 配置。
4. 安装后确认 Provider 是否还在。
5. 重新测试模型切换。

> 注意：只从官网或 GitHub Releases 下载 CC Switch。

## 11. 如何更新 Homebrew / Git / Node / Python

更新 Homebrew 索引：

```bash
brew update
```

升级软件：

```bash
brew upgrade
```

检查版本：

```bash
git --version
node --version
python3 --version
```

> 注意：如果项目依赖特定 Node.js 或 Python 版本，不要在生产项目中贸然升级。先备份，再按项目说明操作。

## 12. 配置备份与恢复

建议备份目录：

```text
~/AI-Tools/Backup/
```

建议备份：

| 内容 | 建议 |
| --- | --- |
| CC Switch Provider 列表 | 可截图或导出，但必须打码 API Key |
| Provider Name | 保存 |
| Base URL | 保存 |
| Model Name | 保存 |
| API Key | 不建议明文保存，只记录存放位置 |
| Claude Code settings | 备份前确认没有密钥 |
| 项目目录 | 重要项目使用 Git 管理 |

备份模板：

```markdown
# 模型配置备份模板

## Provider Name
DeepSeek

## Base URL
以官方文档为准

## Model Name
以官方文档为准

## API Key
不在文档中保存，只记录存放位置

## 备注
用于 Claude Code 日常代码任务
```

恢复流程：

1. 安装 Homebrew。
2. 安装 Git、Claude Code、CC Switch。
3. 恢复 Provider 配置。
4. 重新填写 API Key。
5. Apply / Switch。
6. 重启 Claude Code。
7. 测试读写文件和模型回复。

## 13. 常见错误排查总表

| 现象 | 可能原因 | 解决方法 |
| --- | --- | --- |
| `brew: command not found` | Homebrew 未安装或 PATH 异常 | 按官网安装或修复 PATH |
| `claude: command not found` | Claude Code 未安装或 PATH 未刷新 | 重启 Terminal，检查官方安装步骤 |
| `git: command not found` | Git 未安装 | 使用 Homebrew 或官方方式安装 Git |
| API Key error | Key 错误、过期或泄露 | 重新生成 Key |
| 401 | API Key 错误 | 检查 Key 和鉴权方式 |
| 403 | 无权限或余额不足 | 检查账号权限和余额 |
| 404 | Base URL 或模型名错误 | 查官方文档修正 |
| 429 | 频率限制或余额不足 | 降低频率或检查额度 |
| 500 | 平台服务异常 | 稍后重试或换 Provider |
| `model not found` | 模型名错误或账号无权限 | 更新模型名 |
| CC Switch 切换不生效 | 没 Apply 或没重启 Claude Code | Apply 后重启 |
| 应用无法打开 | macOS 安全限制 | 确认来源后在隐私与安全中允许 |
| 中文路径异常 | 路径编码或转义问题 | 使用英文路径 |
| 能聊天但不能改代码 | 工具调用不兼容 | 换 coding 模型或官方 Claude 对比 |

## 14. 故障定位流程

### 第一步：Claude Code 能否启动

```bash
claude --version
claude
```

不能启动时，检查安装、PATH、网络和官方文档。

### 第二步：Homebrew / Git 是否正常

```bash
brew --version
git --version
```

异常时先修复 Homebrew 和 Git。

### 第三步：模型接口是否正常

检查：

- API Key。
- Base URL。
- Model Name。
- 平台余额。
- 平台状态。

### 第四步：CC Switch 是否切换成功

检查：

- 当前 Provider。
- 是否 Apply / Switch。
- 是否重启 Claude Code。
- 环境变量是否被旧配置覆盖。

### 第五步：是否是模型能力问题

表现：

- 能聊天但不能工具调用。
- 能回复但不能改文件。
- 代码质量差。
- 长任务容易中断。

处理：

- 换更适合 coding 的模型。
- 换官方推荐接口。
- 切回官方 Claude 模型做对比。

## 15. 日常使用规范

1. 每个项目单独建文件夹。
2. 不要把项目乱放在桌面。
3. 路径尽量使用英文。
4. 不要把 API Key 写进项目。
5. 不要把 API Key 发给别人。
6. 做代码项目前先 Git 初始化。
7. 修改重要项目之前先备份。
8. Claude Code 执行高风险命令前要看清楚。
9. 不要随便允许删除文件命令。
10. 切换模型后要重新打开 Claude Code。

推荐目录：

```text
~/AI-Tools/
├── Projects/
│   ├── python-demo/
│   ├── web-demo/
│   └── docs-demo/
├── Docs/
└── Backup/
```

## 16. 每周维护清单

- [ ] 检查 `brew --version`
- [ ] 检查 `git --version`
- [ ] 检查 `node --version`
- [ ] 检查 `python3 --version`
- [ ] 检查 `claude --version`
- [ ] 检查 CC Switch 是否能打开
- [ ] 检查常用 Provider 是否可用
- [ ] 检查 API 余额
- [ ] 检查模型名是否更新
- [ ] 备份重要配置
- [ ] 确认 API Key 未泄露

## 17. 出问题时发给技术支持的信息模板

```text
系统版本：
macOS 版本：

Mac 芯片：
Apple Silicon / Intel

Claude Code 版本：
运行 claude --version 的结果：

Homebrew 版本：
运行 brew --version 的结果：

Git 版本：
运行 git --version 的结果：

使用的 Provider：
DeepSeek / Qwen / GLM / Kimi / SiliconFlow / OpenRouter / 其他

Base URL：
只发域名或地址，不发 API Key

模型名：
例如 deepseek-chat

报错截图：
请打码 API Key

问题描述：
什么时候开始出现？
之前是否正常？
是否刚刚更新过软件？
是否刚刚切换过模型？
```

> 注意：截图给技术支持前必须打码 API Key，不要把终端里包含 Key 的输出直接发出。

## 18. 维护版最简自检流程

```bash
brew --version
git --version
claude --version
echo $ANTHROPIC_BASE_URL
claude
```

进入 Claude Code 后输入：

```text
请创建 health_check.md，写入“环境正常”。
```

如果文件创建成功，说明 Claude Code 能启动、当前目录能读写、模型能响应，基础环境正常。失败时按本指南的排查流程处理。
