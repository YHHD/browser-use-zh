---
name: cloud
description: >
  Browser Use Cloud 的文档参考 — 托管 API 和用于浏览器自动化的 SDK。当用户需要帮助 Cloud REST API（v2 或 v3）、browser-use-sdk（Python 或 TypeScript）、X-Browser-Use-API-Key 身份验证、云会话、浏览器配置文件、配置文件同步、CDP WebSocket 连接、隐身浏览器、住宅代理、验证码处理、webhook、工作区、技能市场、liveUrl 流式传输、定价或集成模式（聊天 UI、子代理、向现有代理添加浏览器工具）时使用。也可用于 n8n/Make/Zapier 集成、在云基础设施上使用 Playwright/Puppeteer/Selenium 或 1Password vault 集成的问题。不用于开源 Python 库（Agent、Browser、Tools 配置）— 请改用开源技能。
allowed-tools: Read
---

# Browser Use Cloud 参考

Cloud REST API、SDK 和集成模式的参考文档。
根据用户需求读取相关文件。

## API 和平台

| 主题 | 读取 |
|------|------|
| 设置、第一个任务、定价、FAQ | `references/quickstart.md` |
| v2 REST API：所有 30 个端点、cURL 示例、模式 | `references/api-v2.md` |
| v3 BU Agent API：会话、消息、文件、工作区 | `references/api-v3.md` |
| 会话、配置文件、身份验证策略、1Password | `references/sessions.md` |
| CDP 直接访问、Playwright/Puppeteer/Selenium | `references/browser-api.md` |
| 代理、webhook、工作区、技能、MCP、实时视图 | `references/features.md` |
| 并行、流式传输、地理抓取、教程 | `references/patterns.md` |

## 集成指南

| 主题 | 读取 |
|------|------|
| 构建带实时浏览器视图的聊天界面 | `references/guides/chat-ui.md` |
| 使用 browser-use 作为子代理（任务输入 → 结果输出） | `references/guides/subagent.md` |
| 向现有代理添加 browser-use 工具 | `references/guides/tools-integration.md` |

## 关键注意事项

- Cloud API 基础 URL：`https://api.browser-use.com/api/v2/`（v2）或 `https://api.browser-use.com/api/v3`（v3）
- 身份验证标头：`X-Browser-Use-API-Key: <key>`
- 获取 API 密钥：https://cloud.browser-use.com/new-api-key
- 设置环境变量：`BROWSER_USE_API_KEY=<key>`
- Cloud SDK：`uv pip install browser-use-sdk`（Python）或 `npm install browser-use-sdk`（TypeScript）
- Python v2：`from browser_use_sdk import AsyncBrowserUse`
- Python v3：`from browser_use_sdk.v3 import AsyncBrowserUse`
- TypeScript v2：`import { BrowserUse } from "browser-use-sdk"`
- TypeScript v3：`import { BrowserUse } from "browser-use-sdk/v3"`
- CDP WebSocket：`wss://connect.browser-use.com?apiKey=KEY&proxyCountryCode=us`
