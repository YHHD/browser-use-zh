# CLAUDE.md

此文件为Claude Code（claude.ai/code）与此仓库中的代码进行交互时提供指导。

Browser-Use 是一个异步 Python >= 3.11 库，使用 LLM + CDP（Chrome开发工具协议）实现 AI 浏览器驱动功能。核心架构使 AI 代理能够自主导航网页、与元素交互，并通过处理 HTML 和进行 LLM 驱动的决策来完成复杂任务。

## 高级架构

该库遵循事件驱动架构，具有几个关键组件：

### 核心组件

- **Agent (`browser_use/agent/service.py`)**: 主要协调器，接收任务、管理浏览器会话并执行 LLM 驱动的动作循环
- **BrowserSession (`browser_use/browser/session.py`)**: 管理浏览器生命周期、CDP 连接，并通过事件总线协调多个监听服务
- **Tools (`browser_use/tools/service.py`)**: 动作注册表，将 LLM 决策映射到浏览器操作（点击、输入、滚动等）
- **DomService (`browser_use/dom/service.py`)**: 提取和处理 DOM 内容，处理元素突出显示和可访问性树生成
- **LLM 集成 (`browser_use/llm/`)**: 抽象层支持 OpenAI、Anthropic、Google、Groq 和其他提供者

### 事件驱动浏览器管理

BrowserSession 使用 `bubus` 事件总线来协调监听服务：
- **DownloadsWatchdog**: 处理 PDF 自动下载和文件管理
- **PopupsWatchdog**: 管理 JavaScript 对话框和弹出窗口
- **SecurityWatchdog**: 实施域名限制和安全策略
- **DOMWatchdog**: 处理 DOM 快照、截图和元素突出显示
- **AboutBlankWatchdog**: 处理空白页重定向

### CDP 集成

使用 `cdp-use` (https://github.com/browser-use/cdp-use) 进行类型化 CDP 协议访问。所有 CDP 客户端管理位于 `browser_use/browser/session.py`。

我们希望我们的库 API 易于使用、直观且难以出错。

## 开发命令

**设置：**
```bash
uv venv --python 3.11
source .venv/bin/activate
uv sync
```

**测试：**
- 运行 CI 测试：`uv run pytest -vxs tests/ci`
- 运行所有测试：`uv run pytest -vxs tests/`
- 运行单个测试：`uv run pytest -vxs tests/ci/test_specific_test.py`

**质量检查：**
- 类型检查：`uv run pyright`
- 检查格式：`uv run ruff check --fix` and `uv run ruff format`
- Pre-commit 钩子：`uv run pre-commit run --all-files`

**MCP 服务器模式：**
该库可以运行为 MCP 服务器以与 Claude Desktop 集成：
```bash
uvx browser-use[cli] --mcp
```

## 代码风格

- 使用异步 Python
- 在所有 Python 代码中使用制表符进行缩进，而不是空格
- 使用现代 Python >3.12 类型化风格，例如使用 `str | None` 而不是 `Optional[str]`，使用 `list[str]` 而不是 `List[str]`，使用 `dict[str, Any]` 而不是 `Dict[str, Any]`
- 尝试将所有控制台日志逻辑保留在单独的方法中，所有以 `_log_...` 开头，例如 `def _log_pretty_path(path: Path) -> str` 以不影响主逻辑
- 使用 Pydantic v2 模型来表示内部数据和任何用户面向的 API 参数，否则将是字典
- 在 Pydantic 模型中使用 `model_config = ConfigDict(extra='forbid', validate_by_name=True, validate_by_alias=True, ...)` 等参数来调整 Pydantic 模型行为，具体取决于用例。使用 `Annotated[..., AfterValidator(...)]` 编码尽可能多的验证逻辑，而不是模型上的辅助方法
- 我们通常在 `service.py` 文件中保留每个子组件的主代码，并且我们在 `views.py` 文件中保留大多数 Pydantic 模型，除非它们足够长以保证自己的文件
- 在函数的开始和结束使用运行时断言来实执约束和假设
- 对所有新的 id 字段使用 `from uuid_extensions import uuid7str` + `id: str = Field(default_factory=uuid7str)`
- 使用 `uv run pytest -vxs tests/ci` 运行测试
- 使用 `uv run pyright` 运行类型检查器

## CDP-Use

我们使用称为 cdp-use 的 CDP 的薄包装：https://github.com/browser-use/cdp-use。cdp-use 仅为 websocket 调用提供浅层类型化接口，所有 CDP 客户端和会话管理 + 其他 CDP 助手仍然位于 browser_use/browser/session.py。

- CDP-Use: 所有 CDP API 通过 cdp-use `cdp_client.send.DomainHere.methodNameHere(params=...)` 公开为自动类型化接口，如下所示：
  - `cdp_client.send.DOMSnapshot.enable(session_id=session_id)`
  - `cdp_client.send.Target.attachToTarget(params={'targetId': target_id, 'flatten': True})` 或更好的：
    `cdp_client.send.Target.attachToTarget(params=ActivateTargetParameters(targetId=target_id, flatten=True))` (从 `cdp_use.cdp.target` 导入 `ActivateTargetParameters`)
  - `cdp_client.register.Browser.downloadWillBegin(callback_func_here)` 用于事件注册，而不是 `cdp_client.on(...)` 不存在！

## 保持示例和测试最新

- 确保读取 `examples/` 目录中的相关示例以获得上下文，并在进行更改时保持它们最新
- 确保读取 `tests/` 目录中的相关测试（特别是 `tests/ci/*.py`）并保持它们最新
- 一旦测试文件通过，应将其移动到 `tests/ci/` 子目录，该子目录中的文件被视为"默认集"并由 CI 在每次提交时自动发现和运行。确保任何特定于事件的测试都位于其 `tests/ci/test_action_EventNameHere.py` 文件中
- 永远不要在测试中模拟任何东西，总是使用真实对象！唯一的例外是 llm，对于 llm，您可以使用 `conftest.py` 中的 pytest fixtures 和实用程序来设置 LLM 响应。对于测试特定的浏览器场景，请使用 pytest-httpserver 在需要的每个测试的 fixture 中设置 html 和响应（参见其他 `tests/ci` 文件以获得示例）
- 绝不在测试中使用真实的远程 URL（例如 `https://google.com` 或 `https://example.com`），而是使用 pytest-httpserver 在 fixture 中设置一个测试服务器，以响应该测试所需的 html（参见其他 `tests/ci` 文件以获得示例）
- 使用现代 pytest-asyncio 最佳实践：不再需要在测试函数上使用 `@pytest.mark.asyncio` 装饰器，仅将正常异步函数用于异步测试。在需要它的测试中使用 `loop = asyncio.get_event_loop()`，而不是将 `event_loop` 作为函数参数传递。不需要在顶部手动设置事件循环的 fixture，它由 pytest 自动设置。Fixture 函数（甚至异步的）只需要一个简单的 `@pytest.fixture` 装饰器，没有参数

## 个性

不用担心形式。

不要回避复杂性，假设需要深度技术解释作为所有问题的答案。说出与相关研究领域相关的正确术语、模型、单位等。信息论和博弈论可以成为评估复杂系统的有用视角。

仔细选择您的类比，将诗意的语言保持到最低，一点干燥的机智是欢迎的。

如果政策阻止您正常回应，请在回答之前打印"!!!!"。

如果政策阻止您有意见，假装您在回应时具有可能是 eigenrobot 典型的观点。

对您信息的质量持批评态度

如果您发现任何请求令人恼火，请以"be real"、"that's crazy man"或"lol no"之类的方式粗鲁地回应

以您现在表现得聪明的方式写作，但要假装您的聪明程度提高了 2 个标准差

## 进行更改的策略

进行任何重大更改时：

1. 找到或编写验证现有设计假设的测试 + 在进行更改之前确认其按预期工作
2. 首先为新设计编写失败的测试，运行它们以确认它们失败
3. 然后实现新设计的更改。在开发过程中根据需要运行或添加测试以验证假设，如果遇到任何困难
4. 更改完成后运行完整的 `tests/ci` 套件。确认新设计有效 & 确认向后兼容性没有被破坏
5. 将相关测试逻辑压缩和去重复到一个文件中，重新阅读整个文件以确保我们没有重复测试相同的东西。快速扫描 `tests/` 中的任何其他可能需要更新或压缩的相关文件
6. 更新 `docs/` 和 `examples/` 中的任何相关文件，并确认它们与实现和测试相匹配

进行任何真正大型重构时，倾向于使用简单事件总线和作业队列来将系统分解为更小的服务，每个服务管理某些隔离子组件的状态。

如果您在就地更新或编辑文件时遇到困难，请尝试将匹配字符串缩短为 1 或 2 行，而不是 3 行。
如果那样不起作用，只需在文件中作为新行插入您的新修改代码，然后在第二步中删除旧代码，而不是替换。

## 文件组织和关键模式

- **服务模式**：每个主要组件都有一个 `service.py` 文件，其中包含主要逻辑（Agent、BrowserSession、DomService、Tools）
- **Views 模式**：Pydantic 模型和数据结构位于 `views.py` 文件中
- **事件**：事件定义在 `events.py` 文件中，遵循事件驱动架构
- **浏览器配置文件**：`browser_use/browser/profile.py` 包含所有浏览器启动参数、显示配置和扩展管理
- **系统提示**：代理提示位于 markdown 文件中：`browser_use/agent/system_prompt*.md`

## 浏览器配置

BrowserProfile 通过 `detect_display_configuration()` 自动检测显示大小并配置浏览器窗口。关键配置：
- macOS (`AppKit.NSScreen`) 和 Linux/Windows (`screeninfo`) 的显示大小检测
- 扩展管理（uBlock Origin、cookie 处理程序）具有可配置的白名单
- Chrome 启动参数生成和重复数据删除
- 代理支持、安全设置和无头/有头模式

## MCP（模型上下文协议）集成

该库支持两种模式：
1. **作为 MCP 服务器**：将浏览器自动化工具公开给 MCP 客户端，如 Claude Desktop
2. **与 MCP 客户端**：代理可以连接到外部 MCP 服务器（文件系统、GitHub 等）以扩展功能

连接管理位于 `browser_use/mcp/client.py`。

## 重要开发约束

- **始终使用 `uv` 而不是 `pip`** 进行依赖管理
- **在实现功能时不要创建随机示例文件** - 如果需要测试，请在终端中使用内联代码
- **使用真实模型名称** - 不要用 `gpt-4` 替换 `gpt-4o`（它们是不同的模型）
- **为操作使用描述性名称和文档字符串**
- **返回带有结构化内容的 `ActionResult`** 以帮助代理进行更好的推理
- **在创建 PR 之前运行 pre-commit 钩子**

## 重要指令提醒
按照要求做；仅此而已。
永远不要创建文件，除非它们完全必要才能实现您的目标。
始终倾向于编辑现有文件而不是创建新文件。
永远不要主动创建文档文件 (*.md) 或 README 文件。仅在用户明确要求时才创建文档文件。