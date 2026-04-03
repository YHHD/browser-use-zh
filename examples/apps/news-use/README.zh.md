# News-Use

使用浏览器代理和 Google Gemini 自动监控新闻网站并提取最新文章及情感分析。

> [!IMPORTANT]
> 此演示需要 browser-use v0.7.7+。

https://github.com/user-attachments/assets/698757ca-8827-41f3-98e5-c235d6eef69f

## 功能

1. 代理访问任何新闻网站
2. 查找并点击最新的头条文章
3. 提取标题、URL、发布时间和内容
4. 使用情感分析生成简短/长摘要
5. 跨重启的持久去重

## 设置

确保安装了最新版本的 browser-use：
```bash
pip install -U browser-use
```

导出您的 Gemini API 密钥，从以下地址获取：[Google AI Studio](https://makersuite.google.com/app/apikey) 
```
export GEMINI_API_KEY='your-google-api-key-here'
```

克隆仓库并进入应用文件夹
```bash
git clone https://github.com/browser-use/browser-use.git
cd browser-use/examples/apps/news-use
```

## 用法

```bash
# 一次性提取 - 获取最新文章并退出
python news_monitor.py --once

# 持续监控 - 每 5 分钟检查一次（默认）
python news_monitor.py

# 自定义间隔 - 每 60 秒检查一次
python news_monitor.py --interval 60

# 不同的新闻网站
python news_monitor.py --url https://techcrunch.com
