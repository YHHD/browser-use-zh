---
name: browser-use
description: 自动化浏览器交互以进行网络测试、表单填充、屏幕截图和数据提取。当用户需要导航网站、与网页交互、填充表单、截图或从网页提取信息时使用。
allowed-tools: Bash(browser-use:*)
---

# 使用 browser-use CLI 进行浏览器自动化

`browser-use` 命令提供快速、持久的浏览器自动化。后台守护程序在命令之间保持浏览器打开，每次调用的延迟约为 ~50ms。

## 先决条件

```bash
browser-use doctor    # 验证安装
```

有关设置详情，请参阅 https://github.com/browser-use/browser-use/blob/main/browser_use/skill_cli/README.md

## 核心工作流程

1. **导航**：`browser-use open <url>` — 启动无头浏览器并打开页面
2. **检查**：`browser-use state` — 返回可点击元素及其索引
3. **交互**：使用 state 中的索引（`browser-use click 5`，`browser-use input 3 "text"`）
4. **验证**：`browser-use state` 或 `browser-use screenshot` 来确认
5. **重复**：浏览器在命令之间保持打开

如果命令失败，请先运行 `browser-use close` 以清除任何损坏的会话，然后重试。

要使用用户的现有 Chrome（保留登录/cookie）：先运行 `browser-use connect`。
要使用云浏览器：先运行 `browser-use cloud connect`。
之后，命令的工作方式相同。

## 浏览器模式

```bash
browser-use open <url>                         # 默认：无头 Chromium（无需设置）
browser-use --headed open <url>                # 可见窗口（用于调试）
browser-use connect                            # 连接到用户的 Chrome（保留登录/cookie）
browser-use cloud connect                      # 云浏览器（零配置，需要 API 密钥）
browser-use --profile "Default" open <url>     # 使用特定配置文件的真实 Chrome
```

在 `connect` 或 `cloud connect` 之后，所有后续命令都转到该浏览器 — 无需额外标志。

## 命令

```bash
# 导航
browser-use open <url>                    # 导航到 URL
browser-use back                          # 在历史记录中返回
browser-use scroll down                   # 向下滚动（--amount N 表示像素）
browser-use scroll up                     # 向上滚动
browser-use tab list                      # 列出所有标签页
browser-use tab new [url]                 # 打开新标签页（空白或带 URL）
browser-use tab switch <index>            # 按索引切换到标签页
browser-use tab close <index> [index...]  # 关闭一个或多个标签页

# 页面状态 — 始终先运行 state 以获取元素索引
browser-use state                         # URL、标题、可点击元素及其索引
browser-use screenshot [path.png]         # 屏幕截图（如果没有路径则为 base64，--full 表示整个页面）
```
