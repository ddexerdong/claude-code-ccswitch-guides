# Claude Code + CC Switch Guides

Cross-platform guides for setting up and maintaining Claude Code, CC Switch, and third-party model providers such as DeepSeek, Qwen, GLM, Kimi, SiliconFlow, and OpenRouter.

本仓库提供 Windows 与 macOS 两套文档入口。先选择你的系统，进入后再选择中文 / English，以及安装配置 / 维护指南。

## Choose Your Platform

| Platform | Start Here | Includes |
| --- | --- | --- |
| Windows | [Windows Guides](docs/windows/) | 中文安装配置、中文维护指南、English setup guide、English maintenance guide |
| macOS | [macOS Guides](docs/mac/) | 中文安装配置、中文维护指南、English setup guide、English maintenance guide |

## What These Guides Cover

- Installing and verifying Claude Code
- Installing Git, Homebrew, Node.js, Python, and recommended development tools
- Installing CC Switch from trusted sources
- Adding providers for DeepSeek, Qwen, GLM, Kimi, SiliconFlow, OpenRouter, New API, and One API
- Maintaining API keys, Base URLs, model names, and environment variables
- Running health checks and troubleshooting common failures

## Who This Is For

- AI coding tool users
- Claude Code users
- Developers who want to switch models with CC Switch
- Users integrating DeepSeek / Qwen / GLM / Kimi or other compatible providers
- Support engineers and teams preparing customer-facing setup docs

## Quick Start

1. Open the platform page: [Windows](docs/windows/) or [macOS](docs/mac/).
2. Choose your language.
3. Follow the setup guide first.
4. Use the maintenance guide for daily checks and troubleshooting.
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
│   │   └── README.md
│   ├── mac/
│   │   └── README.md
│   └── assets/
└── .gitignore
```

## Disclaimer

- This repository is for learning, technical configuration, and documentation reference.
- Actual tool behavior, installation methods, configuration fields, and supported features are defined by the official documentation.
- API pricing, availability, model names, and endpoints may change without notice.
- You are responsible for account security, data security, compliance, and cost control when using third-party model providers.
- This repository does not provide, sell, or endorse any third-party relay service.
