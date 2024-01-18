---

components:
    - rx.DebounceInput
---

```python exec
import reflex as rx
```

# 防抖

Reflex 是一个以后端为中心的框架，对于需要实时提供交互反馈给用户的应用程序可能会产生负面的性能影响。例如，如果你有一个搜索栏，每次按键都向后端发送请求，那么你很可能会遇到卡顿的用户界面。这是因为后端在处理每个按键时需要做很多工作，而前端在更新用户界面之前需要等待后端响应。

使用 `rx.debounce_input` 组件可以在接收用户输入的同时保持前端的响应性，并在一定延迟后将值发送到后端，或者在失焦时发送，或者在按下`Enter`键时发送。

"通常，这个组件用于包装子级的 `rx.input` 或 `rx.text_area`，但大多数接受 `value` 属性和 `on_change` 事件处理程序的子组件都可以与 `rx.debounce_input` 一起使用。"

这个例子只在延迟 1 秒后发送最终的复选框状态给后端。

```python demo exec
class DebounceCheckboxState(rx.State):
    checked: bool = False

def debounce_checkbox_example():
    return rx.hstack(
        rx.cond(
            DebounceCheckboxState.checked,
            rx.text("Checked", color="green"),
            rx.text("Unchecked", color="red"),
        ),
        rx.debounce_input(
            rx.checkbox(
                on_change=DebounceCheckboxState.set_checked,
            ),
            debounce_timeout=1000,
        ),
    )
```

