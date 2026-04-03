# 贡献代理任务

贡献您自己的代理任务，我们将测试代理是否为 CI 测试解决了它们！

## 如何添加任务

1. 在此目录中创建一个新的 `.yaml` 文件（`tests/agent_tasks/`）。
2. 使用以下格式：

```yaml
name: 我的任务名称
task: 描述代理要执行的任务
judge_context:
  - 列出成功标准，每行一个
max_steps: 10
```

## 准则
- 在您的任务和标准中要具体。
- `judge_context` 应列出成功结果的条件。
- 代理的输出将由使用这些标准的 LLM 进行判断。

## 运行测试

要运行所有代理任务：

```bash
pytest tests/ci/test_agent_real_tasks.py
```

---

祝您贡献愉快！
