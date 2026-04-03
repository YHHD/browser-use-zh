# Browser-Use CLI

从命令行进行快速、持久的浏览器自动化。

## 安装

### 先决条件

| 平台 | 要求 |
|----------|-------------|
| **macOS** | Python 3.11+（安装程序将在需要时使用 Homebrew） |
| **Linux** | Python 3.11+（安装程序将在需要时使用 apt） |
| **Windows** | [Git for Windows](https://git-scm.com/download/win)、Python 3.11+ |

### 单行安装（推荐）

**macOS / Linux：**
```bash
curl -fsSL https://browser-use.com/cli/install.sh | bash
```

**Windows**（在 PowerShell 中运行）：
```powershell
& "C:\Program Files\Git\bin\bash.exe" -c 'curl -fsSL https://browser-use.com/cli/install.sh | bash'
```

### 安装后
```bash
browser-use doctor   # 验证安装
browser-use setup    # 运行设置向导（可选）
```

### 生成模板
```bash
browser-use init                          # 交互式模板选择
browser-use init --list                   # 列出可用的模板
browser-use init --template basic         # 生成特定模板
browser-use init --output my_script.py    # 指定输出文件
browser-use init --force                  # 覆盖现有文件
```

### 从源代码
```bash
uv pip install -e .
```

### 手动安装

如果您更倾向于不使用单行安装程序：

```bash
# 1. 安装软件包
uv pip install browser-use

# 2. 安装 Chromium
browser-use install

# 3. 验证
browser-use doctor
```

## 快速开始

```bash
# 打开网页（自动启动浏览器）
browser-use open https://example.com

# 查看可点击元素及其索引
browser-use state

# 按索引点击元素
browser-use click 5

# 在焦点元素中输入文本
browser-use type "Hello World"

# 填充特定输入字段（点击 + 输入）
browser-use input 3 "john@example.com"

# 截图
browser-use screenshot output.png

# 关闭浏览器
browser-use close
```

## 浏览器模式

```bash
# 默认：无头 Chromium
browser-use open https://example.com

# 可见浏览器窗口
browser-use --headed open https://example.com

# 使用您的真实 Chrome 和默认配置文件（具有现有登录/cookie）
browser-use --profile "Default" open https://gmail.com

# 使用特定的 Chrome 配置文件
browser-use --profile "Profile 1" open https://gmail.com
