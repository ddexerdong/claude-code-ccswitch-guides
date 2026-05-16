# Windows Claude Code + CC Switch + 国产模型配置维护指南

> 注意：本文是维护指南，只用于客户后续自查、自维护。不要在不了解影响的情况下执行安装、更新、删除、重置、清空环境变量等操作。涉及官方软件、模型平台、接口地址和配置字段时，以官方文档为准。

## 维护时常用网站

> 注意：CC Switch 只建议从官网或 GitHub Releases 下载。不要从不明网盘、私信链接、广告下载站、二次打包站下载工具。任何要求付款、充值、登录凭据的假冒 CC Switch 都要警惕。

| 序号 | 网站 | 用途 |
| --- | --- | --- |
| 1 | [Claude Code 官方文档](https://code.claude.com/docs/) | 查看安装、配置、权限、更新、环境变量、常见问题。 |
| 2 | [Claude Code Windows / Setup 文档](https://code.claude.com/docs/en/setup) | 查看 Windows、Git Bash、PowerShell、CMD、系统要求等说明。 |
| 3 | [Claude Code 环境变量文档](https://code.claude.com/docs/en/env-vars) | 查看 `ANTHROPIC_API_KEY`、`ANTHROPIC_BASE_URL`、`CLAUDE_CODE_GIT_BASH_PATH` 等变量。 |
| 4 | [Claude Code Settings 文档](https://code.claude.com/docs/en/settings) | 查看 `settings.json`、`/config`、用户配置、项目配置。 |
| 5 | [Claude Code Quickstart](https://code.claude.com/docs/en/quickstart) | 查看基础启动、登录、常用命令和 Windows 终端差异。 |
| 6 | [CC Switch 官方网站](https://ccswitch.io/) | 下载和了解 CC Switch。 |
| 7 | [CC Switch GitHub](https://github.com/farion1231/cc-switch) | 查看源码、说明、更新记录和安全提醒。 |
| 8 | [CC Switch Releases](https://github.com/farion1231/cc-switch/releases) | 下载最新版安装包，查看版本更新。 |
| 9 | [Git for Windows](https://git-scm.com/download/win) | 下载 Git 和 Git Bash。 |
| 10 | [DeepSeek 平台](https://platform.deepseek.com/) | 查看余额、API Key、模型状态。 |
| 11 | [DeepSeek API 文档](https://api-docs.deepseek.com/) | 查看 Base URL、模型名、API 格式。 |
| 12 | [阿里云百炼 / DashScope](https://bailian.console.aliyun.com/) | 管理 Qwen API Key、模型和用量。 |
| 13 | [DashScope 文档](https://help.aliyun.com/zh/model-studio/) | 查看 OpenAI Compatible 接口、模型名、调用方式。 |
| 14 | [智谱 AI 开放平台](https://open.bigmodel.cn/) | 管理 GLM API Key 和模型。 |
| 15 | [Kimi 开放平台](https://platform.moonshot.cn/) | 管理 Kimi API Key 和模型。 |
| 16 | [SiliconFlow](https://siliconflow.cn/) | 管理国产/开源模型 API Key。 |
| 17 | [OpenRouter](https://openrouter.ai/) | 管理多模型聚合接口。 |

## 1. 维护对象说明

这份指南适用于已经完成初次配置的 Windows AI 开发环境。通常包含：

| 对象 | 普通解释 | 维护重点 |
| --- | --- | --- |
| Claude Code | AI 编程工作台 | 能否启动、登录、读写文件、运行命令 |
| Git for Windows / Git Bash | Git 和 Bash 命令环境 | `git` 是否可用，Git Bash 路径是否正确 |
| CC Switch | 模型配置和切换工具 | Provider 是否正确，切换后是否生效 |
| API Key | 调用模型的密码 | 是否有效、是否泄露、是否过期 |
| Base URL | 模型接口地址 | 是否来自官方文档，路径是否正确 |
| Model Name | 具体使用哪个模型 | 是否过期，账号是否有权限 |
| 环境变量 | 系统里的配置开关 | 是否被旧值覆盖，是否泄露敏感信息 |
| 项目目录 | Claude Code 工作目录 | 是否路径简单、可读写、已备份 |

一句话理解：

| 名称 | 类比 |
| --- | --- |
| Claude Code | AI 编程工作台 |
| 国产模型 | AI 大脑 |
| CC Switch | 模型配置和切换工具 |
| API Key | 调用模型的密码 |
| Base URL | 模型接口地址 |
| Model Name | 具体使用哪个模型 |

## 2. 每次使用前的快速检查

### PowerShell 检查

```powershell
git --version
claude --version
echo $env:ANTHROPIC_API_KEY
echo $env:ANTHROPIC_BASE_URL
```

### CMD 检查

```cmd
git --version
claude --version
echo %ANTHROPIC_API_KEY%
echo %ANTHROPIC_BASE_URL%
```

### Git Bash 检查

```bash
git --version
claude --version
echo $ANTHROPIC_API_KEY
echo $ANTHROPIC_BASE_URL
```

正确现象：

| 检查项 | 正常表现 |
| --- | --- |
| Git | 显示 `git version x.x.x` |
| Claude Code | 显示 Claude Code 版本号 |
| API Key | 不为空，或由 CC Switch / 官方登录方式管理 |
| Base URL | 使用第三方模型时不为空，官方登录时可为空 |

> 注意：如果 API Key 显示出来，不要截图发给别人。共享排查信息时必须打码，只保留前后 2 到 4 位或直接写“已配置”。  
> 注意：只使用官方 Claude 登录时，`ANTHROPIC_API_KEY` 和 `ANTHROPIC_BASE_URL` 不一定需要存在。使用 CC Switch 或第三方模型时，再重点检查这些变量和 Provider 配置。

## 3. Claude Code 是否正常

检查命令：

```powershell
claude --version
claude
```

进入 Claude Code 后测试：

```text
请创建 test.md，内容为“Claude Code 环境测试成功”。
```

然后退出后检查：

```powershell
dir
```

正确现象：

| 项目 | 正常表现 |
| --- | --- |
| 启动 | 能进入 Claude Code |
| 文件读写 | 能创建 `test.md` |
| 项目访问 | 能读写当前项目文件 |
| 命令执行 | 能执行 `dir` 等简单命令 |

异常处理：

| 异常 | 处理方法 |
| --- | --- |
| `claude` 不是内部或外部命令 | 重启终端，检查 PATH，确认 Claude Code 已安装成功，以官方文档为准 |
| 进入不了 Claude | 检查网络、终端、账号状态，必要时查看官方排错文档 |
| 无法登录 | 重新运行 `claude` 或在 Claude Code 中使用 `/login`，检查浏览器跳转和账号权限 |
| 无法读写文件 | 检查当前目录权限，避免系统目录、桌面同步目录、中文和特殊字符路径 |
| 权限弹窗很多 | 认真阅读每个权限提示，只允许你理解且安全的操作；权限策略以官方文档为准 |

## 4. Git / Git Bash 是否正常

检查 Git：

```powershell
git --version
```

检查 Git Bash：

```powershell
"C:\Program Files\Git\bin\bash.exe" --version
```

说明：

| 项目 | 说明 |
| --- | --- |
| Git for Windows | Windows 原生使用 Claude Code 推荐安装 Git for Windows |
| Git Bash 常见路径 | `C:\Program Files\Git\bin\bash.exe` |
| 找不到 Git Bash | 可以设置 `CLAUDE_CODE_GIT_BASH_PATH` |

示例配置：

```json
{
  "env": {
    "CLAUDE_CODE_GIT_BASH_PATH": "C:\\Program Files\\Git\\bin\\bash.exe"
  }
}
```

> 注意：具体写入位置以 Claude Code 官方 Settings 文档为准。常见位置包括用户级 `settings.json`、项目级 `.claude\settings.json` 或本地项目配置，但不要把个人密钥写进会提交的项目配置。

## 5. CC Switch 是否正常

检查内容：

| 检查项 | 要看什么 |
| --- | --- |
| 是否能打开 | CC Switch 窗口能正常出现 |
| Provider 列表 | 能看到已配置的 DeepSeek / Qwen / GLM / Kimi 等 Provider |
| 当前 Provider | 当前启用的 Provider 是否是你想用的 |
| API Key | 是否已填写，是否过期，是否属于正确平台 |
| Base URL | 是否和官方文档一致 |
| Model Name | 是否是当前平台仍支持的模型名 |
| Apply / Switch | 是否已经点击启用或切换 |
| Claude Code 重启 | 切换后是否关闭并重新打开 Claude Code |

验证流程：

1. 打开 CC Switch。
2. 切换到 DeepSeek / Qwen / 其他 Provider。
3. 点击 Apply / Switch。
4. 关闭当前 Claude Code。
5. 重新打开终端。
6. 进入项目目录。
7. 运行：

```powershell
claude
```

8. 输入：

```text
请用一句话说明当前模型接口是否响应正常。
```

正确现象：

| 正常项 | 说明 |
| --- | --- |
| 能正常回复 | 模型接口能响应 |
| 没有 API Key error | API Key 基本可用 |
| 没有 `model not found` | 模型名基本正确 |
| 没有 Base URL error | 接口地址基本正确 |
| 没有 401/403/404/429 | 账号权限、余额、频率限制暂未触发 |

## 6. API Key 如何维护

### 什么情况下需要更换 API Key

| 情况 | 说明 |
| --- | --- |
| Key 泄露 | 出现在截图、聊天、GitHub、公开文档中 |
| Key 过期 | 平台显示已过期或被禁用 |
| 平台余额不足 | 充值或更换账号后可能需要新 Key |
| 换了模型平台 | 从 DeepSeek 换到 Qwen、GLM、Kimi 等 |
| 客户换账号 | 原账号不再使用 |
| 报 401 Unauthorized | 常见于 Key 错误或失效 |
| 报 invalid api key | Key 格式、平台或权限错误 |

### 更换流程

1. 登录模型平台官网。
2. 删除旧 Key 或禁用旧 Key。
3. 创建新 Key。
4. 打开 CC Switch。
5. 替换 API Key。
6. Apply / Switch。
7. 重启 Claude Code。
8. 测试回复。

### 安全提醒

> 注意：不要把 API Key 发到微信群、QQ群、朋友圈、公开工单、公开仓库或陌生人提供的网页里。

| 不要做 | 原因 |
| --- | --- |
| 不要截图暴露 API Key | 截图会被转发或留存 |
| 不要提交到 GitHub | 一旦公开可能被自动扫描和盗用 |
| 不要写进 README | README 通常会被分享 |
| 不要发给陌生人 | 对方可能直接消耗你的余额 |
| 不要保存在明文共享文档 | 团队外泄风险高 |

如果怀疑泄露，立即去平台删除旧 Key，生成新 Key，并检查账单和调用记录。

## 7. Base URL 和模型名如何维护

Base URL 是模型接口地址。Model Name 是具体使用的模型名字。

常见问题：

| 问题 | 影响 |
| --- | --- |
| Base URL 错一个字符 | 可能直接不能用 |
| 多写或少写 `/v1` | 可能 404 或请求路径重复 |
| 模型名过期 | 可能 `model not found` |
| 平台更新模型名 | 需要同步修改 CC Switch |
| Compatible 地址不同 | OpenAI Compatible / Anthropic Compatible 地址可能不是同一个 |

维护流程：

1. 打开模型官方文档。
2. 找到 Base URL。
3. 找到 Model Name。
4. 填入 CC Switch。
5. Apply / Switch。
6. 重启 Claude Code。
7. 测试。

> 注意：DeepSeek、Qwen、GLM、Kimi 等模型名可能更新。以官方文档为准，不要迷信旧教程、群聊截图或过期博客。

## 8. 更新维护

### Claude Code 更新

维护原则：

| 项目 | 建议 |
| --- | --- |
| 更新来源 | 优先查看 Claude Code 官方文档 |
| 安装方式 | 如果是官方安装器安装，按官方推荐方式更新 |
| 更新前 | 保存正在进行的工作，关闭 Claude Code 会话 |
| 更新后 | 检查版本和基础功能 |

更新后运行：

```powershell
claude --version
```

> 注意：本文不提供一键更新命令，避免客户误操作。具体更新方式以 Claude Code 官方文档为准。

### Git for Windows 更新

维护原则：

| 项目 | 建议 |
| --- | --- |
| 下载来源 | 只去 Git for Windows 官网 |
| 更新方式 | 下载新版安装包，按官方安装器提示覆盖安装 |
| 更新后 | 重新打开终端检查版本 |

更新后检查：

```powershell
git --version
```

### CC Switch 更新

维护原则：

| 项目 | 建议 |
| --- | --- |
| 下载来源 | 只从 `https://ccswitch.io/` 或 GitHub Releases 下载 |
| 更新前 | 建议备份配置 |
| 更新方式 | 下载新版 Windows 安装包，按官方说明安装 |
| 更新后 | 检查 Provider 配置是否还在 |
| 复测 | 切换模型后重新测试 Claude Code |

> 注意：不要从不明网盘、私信链接、短链接、广告弹窗下载 CC Switch。

### 模型平台更新

定期维护：

| 项目 | 建议 |
| --- | --- |
| API 余额 | 定期检查余额和用量 |
| 模型名 | 定期查看是否变化 |
| 推荐模型 | 查看平台是否推荐新模型 |
| 稳定性 | 若新模型不可用，先换回稳定模型 |
| 接口格式 | 查看 OpenAI Compatible / Anthropic Compatible 是否有变更 |

## 9. 配置备份与恢复

建议备份：

| 内容 | 是否建议保存明文 | 说明 |
| --- | --- | --- |
| CC Switch 配置截图或导出文件 | 可以 | 截图前必须打码 API Key |
| Provider 名称 | 可以 | 例如 DeepSeek、Qwen、Kimi |
| Base URL | 可以 | 不是密钥，但也建议只在内部文档保存 |
| Model Name | 可以 | 便于恢复 |
| API Key | 不建议 | 不在文档中明文保存，只记录存放位置 |
| Claude Code `settings.json` | 可以 | 备份前确认没有密钥 |
| 项目目录 | 可以 | 重要项目建议 Git 管理 |
| README / 使用说明 | 可以 | 便于交接 |

建议目录：

```text
C:\AI-Tools\Backup\
├── ccswitch_provider_list.md
├── claude_settings_backup.json
├── environment_notes.md
└── project_notes.md
```

备份模板：

```markdown
# 模型配置备份模板

## Provider Name
DeepSeek

## Base URL
https://api.deepseek.com

## Model Name
以官方文档为准

## API Key
不在文档中保存，只记录存放位置

## 备注
用于 Claude Code 日常代码任务
```

恢复流程：

1. 安装 Git。
2. 安装 Claude Code。
3. 安装 CC Switch。
4. 恢复 Provider 配置。
5. 重新填写 API Key。
6. Apply / Switch。
7. 测试 Claude Code。

> 注意：恢复时不要直接复制旧电脑里的明文 Key 文档。推荐到平台重新生成 Key，再填入 CC Switch。

## 10. 常见错误排查总表（FAQ）

| 现象 | 可能原因 | 解决方法 |
| --- | --- | --- |
| `claude` 不是内部或外部命令 | PATH 未刷新 / 安装失败 | 重启终端，检查安装，重新安装 |
| `git` 不是内部或外部命令 | 未安装 Git | 安装 Git for Windows |
| `irm` 不识别 | 在 CMD 中运行了 PowerShell 命令 | 换 PowerShell |
| `&&` 报错 | 在 PowerShell 中运行了 CMD 命令 | 换 CMD 或拆成多条命令 |
| API Key error | Key 错误 / 过期 / 泄露 | 重新生成 Key |
| `model not found` | 模型名错误 | 查官方文档更新模型名 |
| 401 | API Key 错误 | 检查 Key |
| 403 | 无权限 / 余额不足 | 检查账号权限和余额 |
| 404 | Base URL 或模型名错误 | 检查地址和模型名 |
| 429 | 频率限制 / 余额不足 | 降低请求频率或充值 |
| 500 | 平台服务异常 | 稍后重试或换平台 |
| 切换模型不生效 | 没 Apply / 没重启 Claude | Apply 后重启 Claude Code |
| 能聊天但不能改代码 | 工具调用不兼容 | 换模型或换兼容接口 |
| 响应很慢 | 网络 / 模型拥堵 | 换节点 / 换模型 / 稍后重试 |
| 中文路径异常 | 路径编码问题 | 换英文路径 |

## 11. 故障定位流程

### 第一步：先判断 Claude Code 是否能启动

```powershell
claude --version
claude
```

如果不能启动：

| 排查项 | 处理 |
| --- | --- |
| 安装 | 确认 Claude Code 已安装 |
| PATH | 关闭并重新打开终端 |
| 终端 | 换 PowerShell 或 CMD 测试 |
| 软件 | 仍失败时按官方文档重新安装或修复 |

### 第二步：判断 Git 是否正常

```powershell
git --version
```

如果 Git 不正常：

| 排查项 | 处理 |
| --- | --- |
| Git 安装 | 安装 Git for Windows |
| Git Bash 路径 | 检查 `C:\Program Files\Git\bin\bash.exe` |
| Claude Code 配置 | 必要时配置 `CLAUDE_CODE_GIT_BASH_PATH` |

### 第三步：判断模型接口是否正常

检查：

| 项目 | 要点 |
| --- | --- |
| API Key | 是否正确、有效、未过期 |
| Base URL | 是否来自官方文档 |
| Model Name | 是否仍然存在 |
| 平台余额 | 是否有余额或额度 |
| 平台状态 | 是否服务异常或维护 |

### 第四步：判断 CC Switch 是否切换成功

检查：

| 项目 | 要点 |
| --- | --- |
| 当前 Provider | 是否是目标 Provider |
| Apply / Switch | 是否已经点击 |
| Claude Code | 是否关闭后重新打开 |
| 环境变量 | 是否被旧配置覆盖 |
| 官方登录 | 是否和自定义 API 配置混用 |

### 第五步：判断是不是模型能力问题

表现：

| 表现 | 可能原因 |
| --- | --- |
| 可以回复但不能工具调用 | 模型或接口不兼容 Claude Code 工具调用 |
| 可以聊天但不会改文件 | Coding 能力或工具格式不稳定 |
| 生成代码质量很差 | 模型不适合 coding |
| 执行命令失败 | 权限、Shell、工具调用格式或模型能力问题 |

解决：

| 方案 | 说明 |
| --- | --- |
| 换更适合 coding 的模型 | 优先选择平台明确推荐的 coding 模型 |
| 换 Anthropic Compatible 接口 | 以平台官方文档为准 |
| 换官方 Claude 模型 | 用于判断是不是第三方模型兼容问题 |
| 使用更稳定 Provider | 保留一个长期稳定的备用配置 |

## 12. 日常使用规范

必须遵守：

1. 每个项目单独建文件夹。
2. 不要在桌面乱放项目。
3. 路径尽量英文。
4. 不要把 API Key 写进项目。
5. 不要把 API Key 发给别人。
6. 做代码项目前先 Git 初始化。
7. 修改重要项目之前先备份。
8. Claude Code 执行高风险命令前要看清楚。
9. 不要随便允许删除文件命令。
10. 切换模型后要重新打开 Claude Code。

推荐目录：

```text
C:\AI-Tools\
├── Projects\
│   ├── python-demo\
│   ├── matlab-demo\
│   └── web-demo\
├── Docs\
└── Backup\
```

高风险命令示例：

| 命令类型 | 风险 |
| --- | --- |
| 删除文件 | 可能误删项目 |
| 清空目录 | 可能删除源码或数据 |
| 覆盖配置 | 可能导致模型无法连接 |
| 上传仓库 | 可能泄露 API Key |
| 修改系统环境变量 | 可能影响所有项目 |

> 注意：看到 Claude Code 准备执行你不理解的命令时，先拒绝或要求它解释命令作用。

## 13. 每周维护清单

- [ ] 检查 `claude --version`
- [ ] 检查 `git --version`
- [ ] 检查 CC Switch 是否能打开
- [ ] 检查常用 Provider 是否可用
- [ ] 检查 API 余额
- [ ] 检查是否有模型名更新
- [ ] 检查是否有 CC Switch 新版本
- [ ] 备份重要配置
- [ ] 清理无用测试项目
- [ ] 确认 API Key 未泄露

## 14. 每次出问题先发给技术支持的信息

客户反馈模板：

```text
系统版本：
Windows 10 / Windows 11

Claude Code 版本：
运行 claude --version 的结果：

Git 版本：
运行 git --version 的结果：

使用的 Provider：
DeepSeek / Qwen / GLM / Kimi / 其他

Base URL：
只发域名，不发 API Key

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

> 注意：绝对不要发完整 API Key。截图前先打码，不要把终端里包含 Key 的内容直接发出。

建议补充：

| 信息 | 示例 |
| --- | --- |
| 终端类型 | PowerShell / CMD / Git Bash |
| 错误码 | 401 / 403 / 404 / 429 / 500 |
| 是否使用 CC Switch | 是 / 否 |
| 当前 Provider | DeepSeek / Qwen / GLM / Kimi / OpenRouter |
| 是否能官方 Claude 登录 | 能 / 不能 / 未测试 |

## 15. 维护版最简自检流程

超短版检查：

```powershell
git --version
claude --version
echo $env:ANTHROPIC_BASE_URL
claude
```

进入 Claude Code 后输入：

```text
请创建 health_check.md，写入“环境正常”。
```

如果文件创建成功，说明：

| 项目 | 结论 |
| --- | --- |
| Claude Code | 能启动 |
| 当前目录 | 能读写 |
| 模型接口 | 能响应 |
| 基础环境 | 正常 |

如果失败，按本指南的 FAQ 和故障定位流程排查。
