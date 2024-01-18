---

components:
    - rx.chakra.TextArea
---

```python exec
import reflex as rx
```

# 文本区域

TextArea 组件允许您轻松创建多行文本输入框。

```python demo exec
class TextareaState(rx.State):
    text: str = "Hello World!"

def textarea_example():
    return rx.vstack(
        rx.heading(TextareaState.text),
        rx.text_area(value=TextareaState.text, on_change=TextareaState.set_text)
    )
```

或者，您可以使用 `on_blur` 事件处理程序，仅在用户点击其他区域时才更新状态。

与 Input 组件类似，当使用完全控制时，TextArea 也使用了防抖输入的实现。
您可以通过设置 `debounce_timeout` 属性来调整防抖延迟。
您可以在 [DebouncedInput]("/docs/library/forms/debounceinput") 组件中找到使用示例。

