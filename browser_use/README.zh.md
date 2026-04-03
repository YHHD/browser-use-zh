# 代码库结构

> 代码结构受到 https://github.com/Netflix/dispatch 的启发。

关于如何构建可扩展代码库的很好结构也在 [此仓库](https://github.com/zhanymkanov/fastapi-best-practices) 中。

这只是一份关于我们应该如何构建后端代码库的简要文档。

## 代码结构

```markdown
src/
/<服务名称>/
models.py
services.py
prompts.py
views.py
utils.py
routers.py

    	/_<子服务名称>/
```

### Service.py

始终为单个文件，除非它变得太长 - 超过约 500 行，将其拆分为 \_子服务

### Views.py

始终将视图拆分为两部分

```python
# 所有内容
...

# 请求
...

# 响应
...
```

如果太长→拆分成多个文件

### Prompts.py

单个文件；如果太长→拆分成多个文件（每个文件一个提示符或类似内容）

### Routers.py

永远不要拆分为多于一个文件
