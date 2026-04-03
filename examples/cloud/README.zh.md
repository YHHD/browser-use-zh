# Browser Use 云示例 🚀

欢迎使用 Browser Use Cloud 示例！此文件夹包含逐步增加复杂度的示例，可帮助您快速高效地开始使用 Browser Use Cloud API。

## 📋 先决条件

1. **API 密钥**：从 [cloud.browser-use.com](https://cloud.browser-use.com/new-api-key) 获取 API 密钥
2. **Python 环境**：Python 3.11+ 及依赖项
3. **环境变量**：配置 API 设置

### 快速设置

```bash
# 创建虚拟环境并安装依赖项（从项目根目录）
uv venv --python 3.11
source .venv/bin/activate  # Windows 上：.venv\Scripts\activate
uv sync

# 设置环境变量
export BROWSER_USE_API_KEY="your_api_key_here"
export BROWSER_USE_BASE_URL="https://api.browser-use.com/api/v1"  # 可选
export BROWSER_USE_TIMEOUT="30"  # 可选：请求超时（以秒为单位）

# 或使用 .env 文件（推荐）
cp examples/cloud/env.example .env
# 用您的值编辑 .env

# 从项目根目录运行示例
python examples/cloud/01_basic_task.py
```

## 🎯 示例概述

### 🚀 简单云设置示例

- **[01_basic_task.py](./01_basic_task.py)** - 您的第一个云任务（从这里开始！）
- **[02_fast_mode_gemini.py](./02_fast_mode_gemini.py)** - ⚡ 使用 Gemini Flash 的超快速模式
- **[03_structured_output.py](./03_structured_output.py)** - 获取结构化 JSON 响应
- **[04_proxy_usage.py](./04_proxy_usage.py)** - 🌍 用于地理限制和验证码解决的代理
- **[05_search_api.py](./05_search_api.py)** - 🔍 用于内容提取的搜索 API（测试版）

## 💰 成本优化提示

1. **使用 Gemini Flash** 以实现最快/最便宜的执行（每步 $0.01）
2. **在不需要验证码解决时禁用代理**
3. **禁用元素突出显示**以获得更好的性能
4. **设置 max_agent_steps** 以防止成本失控
5. **使用结构化输出**以减少解析开销
6. **在生产中添加超时和重试**以实现可靠性
7. **使用域限制**处理机密信息时

## 🎨 快速模式配置

为了获得最大速度和成本效率：

```python
{
    "llm_model": "gemini-2.5-flash",
    "use_proxy": False,
    "highlight_elements": False,
    "use_adblock": True,
    "max_agent_steps": 50
}
```

## 🔐 安全性和高级功能

### 使用代理
```python
{
    "use_proxy": True,
    "proxy_country_code": "us",  # 'us', 'fr', 'it', 'jp', 'au', 'de', 'fi', 'ca'
}
```

### 安全地传递机密
```python
{
    "secrets": {
        "username": "your_username",
        "password": "your_password",
        "api_key": "your_api_key"
    },
    "allowed_domains": ["*.yoursite.com"]  # 推荐与机密一起使用
}
```

## 🔍 搜索 API（测试版）

搜索 API 通过实际浏览网站来提取内容（不是缓存的结果）：

### 简单搜索（多站点）
```python
# 成本：1¢ × 深度 × 网站
{
    "query": "最新 AI 新闻",
    "max_websites": 5,
    "depth": 2
}
```

### URL 搜索（单站点）
```python
# 成本：1¢ × 深度  
{
    "url": "https://example.com",
    "query": "定价信息",
    "depth": 3
}
```

## 🔗 快速链接

- [云 API 文档](https://docs.browser-use.com/cloud)
- [API 参考](https://docs.browser-use.com/api-reference)
- [定价](https://cloud.browser-use.com/billing)
- [Discord 社区](https://link.browser-use.com/discord)

## 🔧 生产最佳实践

- **超时**：所有示例都包含 30 秒的超时和重试逻辑
- **错误处理**：全面的错误捕获和状态代码验证
- **安全性**：在使用机密信息时使用环境变量、域限制
- **可靠性**：内置重试以处理网络问题和限流
- **自动化**：CLI 参数而不是交互式提示，用于 CI/CD

## 🆘 支持

需要帮助？

- 📧 电子邮件：support@browser-use.com
- 💬 Discord：[加入我们的社区](https://link.browser-use.com/discord)
- 📖 文档：<https://docs.browser-use.com>

---

**💡 专业提示**：从 `01_basic_task.py` 开始，逐步深入。每个示例都基于之前的示例！
