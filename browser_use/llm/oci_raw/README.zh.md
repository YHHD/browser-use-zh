# OCI 原始 API 集成

此模块通过原始 API 调用提供与 Oracle Cloud Infrastructure 生成 AI 服务的直接集成，不依赖 Langchain。

## 功能

- **直接 API 集成**：使用 OCI 的原生 Python SDK 进行直接 API 调用
- **异步支持**：完整的异步/等待支持非阻塞操作
- **结构化输出**：支持 Pydantic 模型响应验证
- **错误处理**：带有适当异常类型的全面错误处理
- **身份验证**：支持多种 OCI 身份验证方法

## 安装

确保安装了所需的 OCI 依赖项：

```bash
pip install oci
```

## 用法

### 基本用法

```python
from browser_use import Agent
from browser_use.llm import ChatOCIRaw

# 配置模型
model = ChatOCIRaw(
    model_id="ocid1.generativeaimodel.oc1.us-chicago-1.amaaaaaask7dceya...",
    service_endpoint="https://inference.generativeai.us-chicago-1.oci.oraclecloud.com",
    compartment_id="ocid1.tenancy.oc1..aaaaaaaayeiis5uk2nuubznrekd...",
    provider="meta",  # 或 "cohere"
    temperature=1.0,
    max_tokens=600,
    top_p=0.75,
    auth_type="API_KEY",
    auth_profile="DEFAULT"
)

# 与浏览器使用代理一起使用
agent = Agent(
    task="搜索 Python 教程并总结它们",
    llm=model
)

# 使用 asyncio 运行
import asyncio
history = asyncio.run(agent.run())
```

### 提供者特定的配置示例

#### Meta Llama 模型
```python
meta_model = ChatOCIRaw(
    model_id="ocid1.generativeaimodel.oc1.us-chicago-1.amaaaaaask7dceya...",
    service_endpoint="https://inference.generativeai.us-chicago-1.oci.oraclecloud.com",
    compartment_id="ocid1.tenancy.oc1..aaaaaaaayeiis5uk2nuubznrekd...",
    provider="meta",  # 使用 GenericChatRequest
    temperature=0.7,
    max_tokens=800,
    frequency_penalty=0.0,
    presence_penalty=0.0,
    top_p=0.9
)
```

#### Cohere 模型
```python
cohere_model = ChatOCIRaw(
    model_id="ocid1.generativeaimodel.oc1.us-chicago-1.amaaaaaask7dceya...",
    service_endpoint="https://inference.generativeai.us-chicago-1.oci.oraclecloud.com",
    compartment_id="ocid1.tenancy.oc1..aaaaaaaayeiis5uk2nuubznrekd...",
    provider="cohere",  # 使用 CohereChatRequest
    temperature=1.0,
    max_tokens=600,
    frequency_penalty=0.0,
    top_p=0.75,
    top_k=0  # Cohere 特定参数
)
```

#### xAI 模型
```python
xai_model = ChatOCIRaw(
    model_id="ocid1.generativeaimodel.oc1.us-chicago-1.amaaaaaask7dceya...",
    service_endpoint="https://inference.generativeai.us-chicago-1.oci.oraclecloud.com",
    compartment_id="ocid1.tenancy.oc1..aaaaaaaayeiis5uk2nuubznrekd...",
    provider="xai",  # 使用 GenericChatRequest
    temperature=1.0,
    max_tokens=20000,
    top_p=1.0,
    top_k=0
)
```

### 结构化输出
