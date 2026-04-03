# Langchain 模型（旧版）

此目录包含如何仍然将 Langchain 模型与新 Browser Use 聊天模型一起使用的示例。

## 用法

```python
from langchain_openai import ChatOpenAI

from browser_use import Agent
from .chat import ChatLangchain

async def main():
	"""使用 ChatLangchain 与 OpenAI 通过 LangChain 的基本示例。"""

	# 创建一个 LangChain 模型（OpenAI）
	langchain_model = ChatOpenAI(
		model='gpt-4.1-mini',
		temperature=0.1,
	)

	# 用 ChatLangchain 包装它以使其与 browser-use 兼容
	llm = ChatLangchain(chat=langchain_model)

    agent = Agent(
        task="转到 google.com 并搜索 'Python 浏览器自动化'",
        llm=llm,
    )

    history = await agent.run()

    print(history.history)
```
