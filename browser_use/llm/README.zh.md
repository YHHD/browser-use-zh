# Browser Use LLM

我们官方支持以下 LLM：

- OpenAI
- Anthropic
- Google
- Groq
- Ollama
- DeepSeek
- Mistral

## Mistral 详细信息

将 `ChatMistral` 与 `MISTRAL_API_KEY`（以及可选的 `MISTRAL_BASE_URL`）一起使用。结构化输出会自动删除不支持的 JSON 模式关键字（`minLength`、`maxLength`、`pattern`、`format`），并且生成使用 `max_tokens` 加上可选的 `safe_prompt` 标志。

- Cerebras

## 从 LangChain 迁移

由于我们实现 LLM 的方式，我们在技术上可以支持任何东西。如果您想使用 LangChain 模型，可以使用 `ChatLangchain`（不被官方支持）类。

您可以在 [LangChain 示例](/examples/models/langchain/example.py) 中找到所有详细信息。我们建议您获取该代码并将其用作参考。
