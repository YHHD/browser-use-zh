# Browser Actor

Browser Actor 是一个建立在 CDP（Chrome 开发工具协议）之上的网络自动化库，在 browser-use 生态系统中提供低级浏览器自动化功能。

## 用法

### 与浏览器集成（推荐）
```python
from browser_use import Browser  # BrowserSession 的别名

# 创建并启动浏览器会话
browser = Browser()
await browser.start()

# 创建新标签页并导航
page = await browser.new_page("https://example.com")
pages = await browser.get_pages()
current_page = await browser.get_current_page()
```

### 直接访问页面（高级）
```python
from browser_use.actor import Page, Element, Mouse

# 使用现有浏览器会话创建页面
page = Page(browser_session, target_id, session_id)
```

## 基本操作

```python
# 标签页管理
page = await browser.new_page()  # 创建空白标签页
page = await browser.new_page("https://example.com")  # 创建带 URL 的标签页
pages = await browser.get_pages()  # 获取所有现有标签页
await browser.close_page(page)  # 关闭特定标签页

# 导航
await page.goto("https://example.com")
await page.go_back()
await page.go_forward()
await page.reload()
```

## 元素操作

```python
# 通过 CSS 选择器查找元素
elements = await page.get_elements_by_css_selector("input[type='text']")
buttons = await page.get_elements_by_css_selector("button.submit")

# 通过后端节点 ID 获取元素
element = await page.get_element(backend_node_id=12345)

# AI 驱动的元素查找（需要 LLM）
element = await page.get_element_by_prompt("搜索按钮", llm=your_llm)
element = await page.must_get_element_by_prompt("登录表单", llm=your_llm)
```

> **注意**：`get_elements_by_css_selector` 立即返回，不会等待可见性。

## 元素交互

```python
# 元素操作
await element.click(button='left', click_count=1, modifiers=['Control'])
await element.fill("Hello World")  # 先清除，然后输入
await element.hover()
await element.focus()
await element.check()  # 切换复选框/单选按钮
await element.select_option(["option1", "option2"])  # 用于下拉菜单/选择
await element.drag_to(target_element)  # 拖放

# 元素属性
value = await element.get_attribute("value")
box = await element.get_bounding_box()  # 返回 BoundingBox 或 None
info = await element.get_basic_info()  # 综合元素信息
screenshot_b64 = await element.screenshot(format='png')

# 在元素上执行 JavaScript（此上下文是元素）
text = await element.evaluate("() => this.textContent")
await element.evaluate("(color) => this.style.backgroundColor = color", "yellow")
classes = await element.evaluate("() => Array.from(this.classList)")
```

## 鼠标操作

```python
# 鼠标操作
mouse = await page.mouse
await mouse.click(x=100, y=200, button='left', click_count=1)
await mouse.move(x=300, y=400, steps=1)
await mouse.down(button='left')  # 按下按钮
await mouse.up(button='left')    # 释放按钮
await mouse.scroll(x=0, y=100, delta_x=0, delta_y=-500)  # 在坐标处滚动
```

## 页面操作

```python
# （继续）
```
