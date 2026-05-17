# Claude Code + CC Switch 指南

这是一个用于配置和维护 Claude Code、CC Switch，以及 DeepSeek / Qwen / GLM / Kimi / SiliconFlow / OpenRouter 等模型接口的跨平台教程仓库。

本仓库默认面向中文用户。英文文档请进入：[English Documentation](README.en.md)。

## 文档入口

| 语言 | 文档入口 | 内容 |
| --- | --- | --- |
| 中文 | [中文文档](docs/zh/README.md) | Windows / macOS 安装配置与维护指南 |
| English | [English Documentation](README.en.md) | Windows / macOS setup and maintenance guides |

## 中文快速导航

| 系统 | 安装配置 | 维护指南 |
| --- | --- | --- |
| Windows | [Windows 安装配置](docs/zh/windows/setup.md) | [Windows 维护指南](docs/zh/windows/maintenance.md) |
| macOS | [macOS 安装配置](docs/zh/macos/setup.md) | [macOS 维护指南](docs/zh/macos/maintenance.md) |

## 仓库内容

本仓库覆盖：

- Claude Code 安装、登录、启动和基础使用
- Windows / macOS 开发环境准备
- Git、Git Bash、Homebrew、Node.js、Python 等工具配置
- CC Switch 安装、Provider 配置和模型切换
- DeepSeek / Qwen / GLM / Kimi / SiliconFlow / OpenRouter 等模型接口配置
- API Key、Base URL、Model Name、环境变量维护
- 常见错误排查、自检命令、备份恢复和技术支持反馈模板

## 适合人群

- AI 编程工具使用者
- Claude Code 用户
- 想用 CC Switch 切换模型的用户
- 想接入 DeepSeek / Qwen / GLM / Kimi 等模型接口的用户
- 需要给客户交付配置教程的技术支持或工程团队

## 快速使用

1. 进入 [中文文档](docs/zh/README.md)。
2. 选择 Windows 或 macOS。
3. 第一次配置环境时，阅读“安装配置”。
4. 日常排查问题时，阅读“维护指南”。
5. 发给技术支持前，请打码 API Key、Token、Bearer Token 和敏感请求头。

## 安全提醒

> 注意：不要把 API Key、Token、Bearer Token、账号密码或私密请求头提交到 GitHub。

- 不要把真实 API Key 写进 README、文档、截图、Issue 或工单。
- 不要从不明网盘、私信链接、广告下载站下载 CC Switch。
- CC Switch 只建议从官网或 GitHub Releases 下载。
- 模型 Base URL 和 Model Name 可能变化，必须以官方文档为准。
- 不推荐灰色中转站或不明来源低价接口。
- 如果怀疑 API Key 泄露，请立即到对应模型平台删除旧 Key 并创建新 Key。

## 官方参考

- [Claude Code 官方文档](https://code.claude.com/docs/)
- [Claude Code Quickstart](https://code.claude.com/docs/en/quickstart)
- [Claude Code Setup](https://code.claude.com/docs/en/setup)
- [Claude Code Environment Variables](https://code.claude.com/docs/en/env-vars)
- [Claude Code Settings](https://code.claude.com/docs/en/settings)
- [Anthropic Console](https://console.anthropic.com/)
- [CC Switch 官网](https://ccswitch.io/)
- [CC Switch GitHub](https://github.com/farion1231/cc-switch)
- [CC Switch Releases](https://github.com/farion1231/cc-switch/releases)

## 仓库结构

```text
.
├── README.md
├── README.en.md
├── LICENSE
├── CHANGELOG.md
├── docs/
│   ├── zh/
│   │   ├── windows/
│   │   └── macos/
│   ├── en/
│   │   ├── windows/
│   │   └── macos/
│   ├── assets/
│   └── archive/
└── .gitignore
```

## 免责声明

- 本仓库仅用于个人学习、技术配置和文档参考。
- 具体工具功能、安装方式、配置字段以官方文档为准。
- API 平台费用、可用性、模型名称和接口地址可能变化。
- 使用第三方模型接口需自行承担账号安全、数据安全、合规和费用风险。
- 本仓库不提供、不销售、不背书任何第三方中转服务。
