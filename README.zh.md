<picture>
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/user-attachments/assets/2ccdb752-22fb-41c7-8948-857fc1ad7e24"">
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/user-attachments/assets/774a46d5-27a0-490c-b7d0-e65fcbbfa358">
  <img alt="Shows a black Browser Use Logo in light color mode and a white one in dark color mode." src="https://github.com/user-attachments/assets/2ccdb752-22fb-41c7-8948-857fc1ad7e24"  width="full">
</picture>

<div align="center">
    <picture>
    <source media="(prefers-color-scheme: light)" srcset="https://github.com/user-attachments/assets/9955dda9-ede3-4971-8ee0-91cbc3850125"">
    <source media="(prefers-color-scheme: dark)" srcset="https://github.com/user-attachments/assets/6797d09b-8ac3-4cb9-ba07-b289e080765a">
    <img alt="AI浏览器代理" src="https://github.com/user-attachments/assets/9955dda9-ede3-4971-8ee0-91cbc3850125"  width="400">
    </picture>
</div>

<div align="center">
<a href="https://cloud.browser-use.com"><img src="https://media.browser-use.tools/badges/package" height="48" alt="Browser-Use Package Download Statistics"></a>
</div>

---

<div align="center">
<a href="#demos"><img src="https://media.browser-use.tools/badges/demos" alt="演示"></a>
<img width="16" height="1" alt="">
<a href="https://docs.browser-use.com"><img src="https://media.browser-use.tools/badges/docs" alt="文档"></a>
<img width="16" height="1" alt="">
<a href="https://browser-use.com/posts"><img src="https://media.browser-use.tools/badges/blog" alt="博客"></a>
<img width="16" height="1" alt="">
<a href="https://browsermerch.com"><img src="https://media.browser-use.tools/badges/merch" alt="周边"></a>
<img width="100" height="1" alt="">
<a href="https://github.com/browser-use/browser-use"><img src="https://media.browser-use.tools/badges/github" alt="Github Stars"></a>
<img width="4" height="1" alt="">
<a href="https://x.com/intent/user?screen_name=browser_use"><img src="https://media.browser-use.tools/badges/twitter" alt="Twitter"></a>
<img width="4 height="1" alt="">
<a href="https://link.browser-use.com/discord"><img src="https://media.browser-use.tools/badges/discord" alt="Discord"></a>
<img width="4" height="1" alt="">
<a href="https://cloud.browser-use.com"><img src="https://media.browser-use.tools/badges/cloud" height="48" alt="Browser-Use Cloud"></a>
</div>

</br>

🌤️ 想跳过设置？使用我们的<b>[云服务](https://cloud.browser-use.com)</b>获得更快、可扩展、隐形浏览器自动化！

# 🤖 LLM 快速开始

1. 指导您最喜欢的编码代理（Cursor、Claude Code等）查看 [Agents.md](https://docs.browser-use.com/llms-full.txt)
2. 开始提示！

<br/>

# 👋 人类快速开始

**1. 使用 [uv](https://docs.astral.sh/uv/) (Python>=3.11) 创建环境并安装 Browser-Use：**
```bash
uv init && uv add browser-use && uv sync
# uvx browser-use install  # 如果您没有安装 Chromium，请运行该命令
```

**2. [可选] 从 [Browser Use Cloud](https://cloud.browser-use.com/new-api-key) 获取 API 密钥：**
```
# .env
BROWSER_USE_API_KEY=your-key
# GOOGLE_API_KEY=your-key
# ANTHROPIC_API_KEY=your-key
```

**3. 运行您的第一个代理：**
```python
from browser_use import Agent, Browser, ChatBrowserUse
# from browser_use import ChatGoogle  # ChatGoogle(model='gemini-3-flash-preview')
# from browser_use import ChatAnthropic  # ChatAnthropic(model='claude-sonnet-4-6')
import asyncio

async def main():
    browser = Browser(
        # use_cloud=True,  # 使用 Browser Use Cloud 上的隐形浏览器
    )

    agent = Agent(
        task="查找 browser-use 仓库的星标数量",
        llm=ChatBrowserUse(),
        # llm=ChatGoogle(model='gemini-3-flash-preview'),
        # llm=ChatAnthropic(model='claude-sonnet-4-6'),
        browser=browser,
    )
    await agent.run()

if __name__ == "__main__":
    asyncio.run(main())
```

查看 [库文档](https://docs.browser-use.com/open-source/introduction) 和 [云文档](https://docs.cloud.browser-use.com) 了解更多！

<br/>

# 开源 vs 云服务

<picture>
  <source media="(prefers-color-scheme: light)" srcset="static/accuracy_by_model_light.png">
  <source media="(prefers-color-scheme: dark)" srcset="static/accuracy_by_model_dark.png">
  <img alt="BU Bench V1 - LLM 成功率" src="static/accuracy_by_model_light.png" width="100%">
</picture>

我们在 100 个真实浏览器任务上对 Browser Use 进行了基准测试。完整基准是开源的：**[browser-use/benchmark](https://github.com/browser-use/benchmark)**。

**使用开源版本**
- 您需要 [自定义工具](https://docs.browser-use.com/customize/tools/basics) 或深度代码级集成
- 您想要自托管并在自己的机器上部署浏览器代理

**使用 [云服务](https://cloud.browser-use.com)（推荐）**
- 对于复杂任务有更好的代理（见上图）
- 最简单的起步和扩展方式
- 通过代理轮换和验证码解决方案实现最佳隐形
- 1000+ 集成（Gmail、Slack、Notion 等）
- 持久文件系统和内存

**同时使用两个**
- 使用开源库与您的 [自定义工具](https://docs.browser-use.com/customize/tools/basics)，同时运行我们的 [云浏览器](https://docs.browser-use.com/open-source/customize/browser/remote) 和 [ChatBrowserUse 模型](https://docs.browser-use.com/open-source/supported-models)

<br/>

# 演示


### 📋 表单填充
#### 任务 = "用我的简历和信息填充这份工作申请。"
![工作申请演示](https://github.com/user-attachments/assets/57865ee6-6004-49d5-b2c2-6dff39ec2ba9)
[示例代码 ↗](https://github.com/browser-use/browser-use/blob/main/examples/use-cases/apply_to_job.py)


### 🍎 杂货店购物
#### 任务 = "将这个项目列表添加到我的 Instacart。"

https://github.com/user-attachments/assets/a6813fa7-4a7c-40a6-b4aa-382bf88b1850

[示例代码 ↗](https://github.com/browser-use/browser-use/blob/main/examples/use-cases/buy_groceries.py)


### 💻 个人助手
#### 任务 = "帮我找到自定义 PC 的零件。"

https://github.com/user-attachments/assets/ac34f75c-057a-43ef-ad06-5b2c9d42bf06

[示例代码 ↗](https://github.com/browser-use/browser-use/blob/main/examples/use-cases/pcpartpicker.py)


### 💡 查看 [更多示例 ↗](https://docs.browser-use.com/examples) 并给我们一个星标！

<br/>

# 🚀 模板快速开始

**想更快速地开始？** 生成一个现成可用的模板：

```bash
uvx browser-use init --template default
```

这将创建一个 `browser_use_default.py` 文件，分现成的示例。可用的模板：
- `default` - 最小设置，快速开始
- `advanced` - 所有配置选项和详细注释
- `tools` - 自定义工具和扩展代理的示例

您也可以指定自定义输出路径：
```bash
uvx browser-use init --template default --output my_agent.py
```

<br/>

# 💻 命令行界面（CLI）

从命令行进行快速、持久的浏览器自动化：

```bash
browser-use open https://example.com    # 导航到 URL
browser-use state                       # 查看可点击的元素
browser-use click 5                     # 按索引点击元素
browser-use type "Hello"                # 输入文本
browser-use screenshot page.png         # 截屏
browser-use close                       # 关闭浏览器
```

CLI 在命令之间保持浏览器运行，以便快速迭代。查看 [CLI 文档](browser_use/skill_cli/README.md) 了解所有命令。

### Claude Code 技能

对于 [Claude Code](https://claude.ai/code)，安装技能以启用 AI 辅助浏览器自动化：

```bash
mkdir -p ~/.claude/skills/browser-use
curl -o ~/.claude/skills/browser-use/SKILL.md \
  https://raw.githubusercontent.com/browser-use/browser-use/main/skills/browser-use/SKILL.md
```

<br/>

## 在我们的 [文档 ↗](https://docs.browser-use.com) 上了解集成、托管、自定义工具、MCP 等

<br/>

# FAQ

<details>
<summary><b>最好的模型是什么？</b></summary>

我们为浏览器自动化任务特别优化了**ChatBrowserUse()**。在平均情况下，它以 SOTA 精度的速度完成任务快 3-5 倍。

**定价（每 100 万个 token）：**
- 输入 token：$0.20
- 缓存输入 token：$0.02
- 输出 token：$2.00

对于其他 LLM 提供商，请参阅我们的 [支持的模型文档](https://docs.browser-use.com/supported-models)。
</details>

<details>
<summary><b>我应该在开源预览模型中使用 Browser Use 系统提示吗？</b></summary>

是的。如果您使用 `ChatBrowserUse(model='browser-use/bu-30b-a3b-preview')` 与常规 `Agent(...)`，Browser Use 仍然会为您发送其默认代理系统提示。

您**不**需要添加单独的自定义"Browser Use 系统消息"只是因为您切换到了开源预览模型。仅在您想故意定制默认行为以执行您的任务时，才使用 `extend_system_message` 或 `override_system_message`。

如果您想要最好的默认速度/精度，我们仍然建议使用较新的托管 `bu-*` 模型。如果您想要开源预览模型，除了 `model=` 值，设置保持不变。
</details>

<details>
<summary><b>我可以将自定义工具与代理一起使用吗？</b></summary>

是的！您可以添加自定义工具来扩展代理的功能：

```python
from browser_use import Tools

tools = Tools()

@tools.action(description='描述此工具的作用。')
def custom_tool(param: str) -> str:
    return f"结果：{param}"

agent = Agent(
    task="您的任务",
    llm=llm,
    browser=browser,
    tools=tools,
)
```

</details>

<details>
<summary><b>我可以免费使用吗？</b></summary>

是的！Browser-Use 是开源的并且可以免费使用。您只需要选择一个 LLM 提供商（如 OpenAI、Google、ChatBrowserUse 或使用 Ollama 运行本地模型）。
</details>

<details>
<summary><b>服务条款</b></summary>

这个开源库在 MIT 许可证下授权。关于 Browser Use 服务和数据政策，请参阅我们的 [服务条款](https://browser-use.com/legal/terms-of-service) 和 [隐私政策](https://browser-use.com/privacy/)。
</details>

<details>
<summary><b>我如何处理身份验证？</b></summary>

查看我们的身份验证示例：
- [使用真实浏览器配置文件](https://github.com/browser-use/browser-use/blob/main/examples/browser/real_browser.py) - 重用您的现有 Chrome 配置文件及其保存的登录信息
- 如果您想使用带有收件箱的临时账户，请选择 AgentMail
- 要将您的身份验证配置文件与远程浏览器同步，运行 `curl -fsSL https://browser-use.com/profile.sh | BROWSER_USE_API_KEY=XXXX sh`（用您的 API 密钥替换 XXXX）

这些示例显示了如何无缝地维护会话和处理身份验证。
</details>

<details>
<summary><b>我如何解决 CAPTCHA？</b></summary>

对于 CAPTCHA 处理，您需要更好的浏览器指纹和代理。使用 [Browser Use Cloud](https://cloud.browser-use.com)，它提供设计用来避免检测和 CAPTCHA 验证的隐形浏览器。
</details>

<details>
<summary><b>我如何进入生产阶段？</b></summary>

Chrome 可以消耗大量内存，并且并行运行许多代理可能很难管理。

对于生产用例，使用我们的 [Browser Use Cloud API](https://cloud.browser-use.com)，它处理：
- 可扩展的浏览器基础设施
- 内存管理
- 代理轮换
- 隐形浏览器指纹识别
- 高性能并行执行
</details>

<br/>

<div align="center">

**告诉您的计算机该做什么，它就会完成。**

<img src="https://github.com/user-attachments/assets/06fa3078-8461-4560-b434-445510c1766f" width="400"/>

[![Twitter Follow](https://img.shields.io/twitter/follow/Magnus?style=social)](https://x.com/intent/user?screen_name=mamagnus00)
&emsp;&emsp;&emsp;
[![Twitter Follow](https://img.shields.io/twitter/follow/Gregor?style=social)](https://x.com/intent/user?screen_name=gregpr07)

</div>

<div align="center"> 用❤️制作，位于苏黎世和西小时 </div>