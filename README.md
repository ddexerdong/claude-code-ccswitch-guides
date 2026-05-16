# Claude Code + CC Switch Guides

## 简介

This repository contains cross-platform guides for setting up and maintaining Claude Code, CC Switch, and third-party model providers such as DeepSeek, Qwen, GLM, Kimi, SiliconFlow, and OpenRouter.

这些文档适合用于个人学习、客户交付、团队环境配置和后续维护。文档重点覆盖：

- Claude Code 安装和基础使用
- CC Switch 安装、Provider 配置和模型切换
- DeepSeek / Qwen / GLM / Kimi 等模型接口配置
- API Key、Base URL、Model Name 的安全维护
- Windows 和 macOS 环境自检与故障排查

## 文档目录

| 系统 | 语言 | 类型 | 文档 |
| --- | --- | --- | --- |
| Windows | 中文 | 安装配置 | [Windows 中文安装配置指南](docs/windows/windows_claude_code_ccswitch_full_guide_zh.md) |
| Windows | 中文 | 维护指南 | [Windows 中文维护指南](docs/windows/windows_claude_code_ccswitch_maintenance_zh.md) |
| macOS | 中文 | 安装配置 | [macOS 中文安装配置指南](docs/mac/mac_claude_code_ccswitch_full_guide_zh.md) |
| macOS | 中文 | 维护指南 | [macOS 中文维护指南](docs/mac/mac_claude_code_ccswitch_maintenance_zh.md) |
| Windows | English | Setup Guide | [Windows English Setup Guide](docs/windows/windows_claude_code_ccswitch_full_guide_en.md) |
| Windows | English | Maintenance Guide | [Windows English Maintenance Guide](docs/windows/windows_claude_code_ccswitch_maintenance_en.md) |

## 适合人群

- AI 编程工具使用者
- Claude Code 用户
- 想用 CC Switch 切换模型的用户
- 想接入 DeepSeek / Qwen / GLM / Kimi 等模型的用户
- 需要给客户交付配置教程的人

## 安全提醒

> 注意：不要泄露 API Key、Token、Bearer Token、账号密码或任何私密请求头。

- 不要把密钥提交到 GitHub。
- 不要把密钥写进 README、文档、截图、工单或公开聊天记录。
- 不要从不明来源下载 CC Switch。
- CC Switch 只建议从官网或 GitHub Releases 下载。
- 模型 Base URL 和 Model Name 可能变化，必须以官方文档为准。
- 不推荐灰色中转站或不明来源低价接口。
- 如果怀疑 API Key 泄露，请立即到对应模型平台删除旧 Key 并创建新 Key。

## 使用方式

1. 选择对应系统。
2. 按安装指南完成配置。
3. 用维护指南进行日常自检和排查。
4. 遇到问题先运行文档中的自检命令。
5. 提交技术支持信息前，请先打码 API Key 和 Token。

## 相关官方入口

- [Claude Code Documentation](https://code.claude.com/docs/)
- [Claude Code Quickstart](https://code.claude.com/docs/en/quickstart)
- [Claude Code Setup](https://code.claude.com/docs/en/setup)
- [Claude Code Environment Variables](https://code.claude.com/docs/en/env-vars)
- [Claude Code Settings](https://code.claude.com/docs/en/settings)
- [CC Switch Website](https://ccswitch.io/)
- [CC Switch GitHub](https://github.com/farion1231/cc-switch)
- [CC Switch Releases](https://github.com/farion1231/cc-switch/releases)

## 免责声明

- 本仓库仅为个人学习和技术配置参考。
- 具体工具功能、安装方式、配置字段以官方文档为准。
- API 平台费用、可用性、模型名称和接口地址可能变化。
- 使用第三方模型接口需自行承担账号、安全、费用、合规和数据保护责任。
- 本仓库不提供、不销售、不背书任何第三方中转服务。
