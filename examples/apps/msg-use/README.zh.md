# Msg-Use

使用浏览器代理和 Gemini 的 AI 驱动消息调度程序。用自然语言调度个性化消息，让 AI 智能地撰写它们。

[!WARNING]
此演示需要 browser-use v0.7.7+。

https://browser-use.github.io/media/demos/msg_use.mp4

## 功能

1. 代理自动登录 WhatsApp Web
2. 解析自然语言调度指令
3. 使用 AI 撰写个性化消息
4. 为将来的传送调度消息或立即发送
5. 持久会话（无需重复扫描 QR 代码）

## 设置

确保安装了最新版本的 browser-use：
```bash
pip install -U browser-use
```

导出您的 Gemini API 密钥，从以下地址获取：[Google AI Studio](https://makersuite.google.com/app/apikey)
```
export GOOGLE_API_KEY='your-gemini-api-key-here'
```

克隆仓库并进入应用文件夹
```bash
git clone https://github.com/browser-use/browser-use.git
cd browser-use/examples/apps/msg-use
```

## 初始登录

首次设置需要扫描 QR 代码：
```bash
python login.py
```
- 浏览器打开时扫描 QR 代码
- 会话将保存以供将来使用

## 正常使用

1. **编辑您的日程**在 `messages.txt`：
```
- 在 09.09 18:15 发送"你好"给 Magnus
- 在 20:00 告诉 Camila 我想她
- 提醒妈妈下周二去取车
```

2. **测试模式** - 查看将发送的内容：
```bash
python scheduler.py --test
```

3. **运行调度程序**：
```bash
python scheduler.py

# 调试模式 - 查看浏览器的操作
python scheduler.py --debug

# 自动模式 - 每 ~30 分钟响应一条未读消息
python scheduler.py --auto
```

## 编程用法

```python
import asyncio
from scheduler import schedule_messages

async def main():
    messages = [
        "在 15:30 给 John 发送 hello",
        "在明天早上 9 点提醒 Sarah 开会"
    ]
    await schedule_messages(messages, debug=False)

asyncio.run(main())
```

## 输出

示例调度输出：
```json
[
  {
    "contact": "Magnus",
    "original_message": "Hi",
    "composed_message": "Hi",
    "scheduled_time": "2025-06-13 18:15"
  },
  {
    "contact": "Camila",
    "original_message": "I miss her",
    "composed_message": "我想你 ❤️",
    "scheduled_time": "2025-06-14 20:00"
  }
]
```

## 文件

- `scheduler.py` - 主调度程序脚本
- `login.py` - 一次性登录设置  
- `messages.txt` - 您的自然语言消息计划

## 许可证

MIT
