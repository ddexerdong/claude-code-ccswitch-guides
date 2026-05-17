# Claude Code + CC Switch Guides

Cross-platform setup and maintenance guides for Claude Code, CC Switch, and third-party model providers such as DeepSeek, Qwen, GLM, Kimi, SiliconFlow, and OpenRouter.

本仓库整理了 Windows 与 macOS 上配置 Claude Code、使用 CC Switch 切换模型、维护 API Key / Base URL / Model Name、以及排查常见问题的中英文文档，适合个人学习、客户交付和团队内部环境标准化。

## Documentation

| System | Language | Type | Document |
| --- | --- | --- | --- |
| Windows | 中文 | 安装配置 | [Windows 中文安装配置指南](docs/windows/windows_claude_code_ccswitch_full_guide_zh.md) |
| Windows | 中文 | 维护指南 | [Windows 中文维护指南](docs/windows/windows_claude_code_ccswitch_maintenance_zh.md) |
| Windows | English | Setup Guide | [Windows English Setup Guide](docs/windows/windows_claude_code_ccswitch_full_guide_en.md) |
| Windows | English | Maintenance Guide | [Windows English Maintenance Guide](docs/windows/windows_claude_code_ccswitch_maintenance_en.md) |
| macOS | 中文 | 安装配置 | [macOS 中文安装配置指南](docs/mac/mac_claude_code_ccswitch_full_guide_zh.md) |
| macOS | 中文 | 维护指南 | [macOS 中文维护指南](docs/mac/mac_claude_code_ccswitch_maintenance_zh.md) |
| macOS | English | Setup Guide | [macOS English Setup Guide](docs/mac/mac_claude_code_ccswitch_full_guide_en.md) |
| macOS | English | Maintenance Guide | [macOS English Maintenance Guide](docs/mac/mac_claude_code_ccswitch_maintenance_en.md) |

## What Is Covered

- Installing and verifying Claude Code on Windows and macOS
- Installing Git, Homebrew, Node.js, Python, and other recommended tooling
- Installing CC Switch from trusted sources
- Adding providers for DeepSeek, Qwen, GLM, Kimi, SiliconFlow, OpenRouter, New API, and One API
- Maintaining API keys, Base URLs, model names, and environment variables
- Running health checks before daily use
- Troubleshooting common setup, login, provider, and model-switching issues

## Who This Is For

- AI coding tool users
- Claude Code users
- Developers who want to switch models with CC Switch
- Users integrating DeepSeek / Qwen / GLM / Kimi or other compatible providers
- Consultants, support engineers, and teams preparing customer-facing setup docs

## Quick Start

1. Choose your operating system and language from the documentation table.
2. Follow the setup guide first.
3. Use the maintenance guide for daily checks and troubleshooting.
4. If model switching fails, verify API Key, Base URL, Model Name, and whether Claude Code was restarted.
5. Before asking for support, redact all API keys, tokens, and sensitive headers.

## Security Notes

> Never commit API keys, tokens, bearer tokens, account passwords, or private headers to GitHub.

- Do not write real API keys in README files, documentation, screenshots, issues, or support tickets.
- Do not download CC Switch from unknown cloud-drive links, private-message links, or repackaged installers.
- Download CC Switch only from the official website or GitHub Releases.
- Base URLs and model names can change; always refer to the provider's official documentation.
- This repository does not recommend gray-market relay services or unknown low-cost proxy providers.
- If an API key may have leaked, revoke it immediately on the provider platform and create a new one.

## Official References

- [Claude Code Documentation](https://code.claude.com/docs/)
- [Claude Code Quickstart](https://code.claude.com/docs/en/quickstart)
- [Claude Code Setup](https://code.claude.com/docs/en/setup)
- [Claude Code Environment Variables](https://code.claude.com/docs/en/env-vars)
- [Claude Code Settings](https://code.claude.com/docs/en/settings)
- [Anthropic Console](https://console.anthropic.com/)
- [CC Switch Website](https://ccswitch.io/)
- [CC Switch GitHub](https://github.com/farion1231/cc-switch)
- [CC Switch Releases](https://github.com/farion1231/cc-switch/releases)

## Repository Structure

```text
.
├── README.md
├── LICENSE
├── CHANGELOG.md
├── docs/
│   ├── windows/
│   ├── mac/
│   └── assets/
└── .gitignore
```

## Disclaimer

- This repository is for learning, technical configuration, and documentation reference.
- Actual tool behavior, installation methods, configuration fields, and supported features are defined by the official documentation.
- API pricing, availability, model names, and endpoints may change without notice.
- You are responsible for account security, data security, compliance, and cost control when using third-party model providers.
- This repository does not provide, sell, or endorse any third-party relay service.
