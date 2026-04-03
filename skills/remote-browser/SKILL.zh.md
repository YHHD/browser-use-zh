---
name: remote-browser
description: 从沙盒远程机器控制本地浏览器。当代理在沙盒（无 GUI）中运行并需要导航网站、与网页交互、填充表单、截图或通过隧道暴露本地开发服务器时使用。
allowed-tools: Bash(browser-use:*)
---

# 沙盒代理的浏览器自动化

此技能适用于需要控制无头浏览器的**沙盒远程机器**上运行的代理（云 VM、CI、编码代理）。

## 先决条件

```bash
browser-use doctor    # 验证安装
```

有关设置详情，请参阅 https://github.com/browser-use/browser-use/blob/main/browser_use/skill_cli/README.md

## 核心工作流程

1. **导航**：`browser-use open <url>` — 如果需要启动无头浏览器
2. **检查**：`browser-use state` — 返回可点击元素及其索引
3. **交互**：使用 state 中的索引（`browser-use click 5`，`browser-use input 3 "text"`）
4. **验证**：`browser-use state` 或 `browser-use screenshot` 来确认
5. **重复**：浏览器在命令之间保持打开
6. **清理**：完成时通过 `browser-use close`

## 浏览器模式

```bash
browser-use open <url>                                    # 默认：无头 Chromium
browser-use cloud connect                                 # 配置云浏览器并连接
browser-use --connect open <url>                          # 通过 CDP 自动发现运行的 Chrome
browser-use --cdp-url ws://localhost:9222/... open <url>  # 通过 CDP URL 连接
```

## 命令

```bash
# 导航
browser-use open <url>                    # 导航到 URL
browser-use back                          # 在历史记录中返回
browser-use scroll down                   # 向下滚动（--amount N 表示像素）
browser-use scroll up                     # 向上滚动
browser-use tab list                      # 列出所有标签页和锁定状态
browser-use tab new [url]                 # 打开新标签页（空白或带 URL）
browser-use tab switch <index>            # 按索引切换到标签页
browser-use tab close <index> [index...]  # 关闭一个或多个标签页

# 页面状态 — 始终先运行 state 以获取元素索引
browser-use state                         # URL、标题、可点击元素及其索引
browser-use screenshot [path.png]         # 屏幕截图（如果没有路径则为 base64，--full 表示整个页面）

# 交互 — 使用 state 中的索引
browser-use click <index>                 # 按索引点击元素
browser-use click <x> <y>                 # 在像素坐标处点击
browser-use type "text"                   # 在焦点元素中输入
browser-use input <index> "text"          # 点击元素，然后输入
browser-use keys "Enter"                  # 发送键盘按键（也可以是 "Control+a" 等）
browser-use select <index> "option"       # 选择下拉选项
```
