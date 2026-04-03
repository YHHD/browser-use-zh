# Ad-Use

使用浏览器代理、Google 的 Nano Banana 🍌 和 Veo3 从任何登录页面自动生成 Instagram 图像广告和 TikTok 视频广告。

> [!WARNING]
> 此演示需要 browser-use v0.7.7+。

https://github.com/user-attachments/assets/7fab54a9-b36b-4fba-ab98-a438f2b86b7e

## 功能

1. 代理访问您的目标网站
2. 捕获品牌名称、标语和关键卖点
3. 拍摄干净的屏幕截图作为设计参考
4. 使用 🍌 创建吸引眼球的 Instagram 图像广告
5. 使用 Veo3 生成病毒式 TikTok 视频广告
6. 支持并行生成多个广告

## 设置

确保安装了最新版本的 browser-use（具有屏幕截图功能）：
```bash
pip install -U browser-use
```

导出您的 Gemini API 密钥，从以下地址获取：[Google AI Studio](https://makersuite.google.com/app/apikey) 
```
export GOOGLE_API_KEY='your-google-api-key-here'
```

克隆仓库并进入应用文件夹
```bash
git clone https://github.com/browser-use/browser-use.git
cd browser-use/examples/apps/ad-use
```

## 正常使用

```bash
# 基础 - 生成 Instagram 图像广告（默认）
python ad_generator.py --url https://www.apple.com/iphone-17-pro/

# 使用 Veo3 生成 TikTok 视频广告
python ad_generator.py --tiktok --url https://www.apple.com/iphone-17-pro/

# 并行生成多个广告
python ad_generator.py --instagram --count 3 --url https://www.apple.com/iphone-17-pro/
python ad_generator.py --tiktok --count 2 --url https://www.apple.com/iphone-17-pro/

# 调试模式 - 查看浏览器的操作
```
