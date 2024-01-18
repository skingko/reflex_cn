---
components:
    - rx.radix.themes.Button
---

```python exec
import reflex as rx
import reflex.components.radix.themes as rdxt
```
 
# 按钮

按钮是应用程序用户界面中的基本元素，用户可以点击触发事件。此组件使用了 Radix 的 [button](https://radix-ui.com/primitives/docs/components/button) 组件。

## 基本示例

```python demo
rdxt.button("Click me")
```

### 带图标

```python demo
rdxt.button(
    rdxt.icon(tag="heart"),
    "Like",
    color_scheme="red",
)
```

## 属性

### 禁用

`disabled` 属性禁用按钮，默认值为 `False`。禁用的按钮不会响应用户的交互操作，如点击和无法获取焦点。

```python demo
rx.hstack(
    rdxt.button("Enabled"),
    rdxt.button("Disabled", disabled=True),
)
```

## 触发器

### 点击事件

当按钮被点击时，调用 `on_click` 触发器。

```python demo
rdxt.button("Click me", on_click=rx.window_alert("Clicked!"))
```

## 真实世界示例

```python demo exec
class CountState(rx.State):
    count: int = 0

    def increment(self):
        self.count += 1

    def decrement(self):
        self.count -= 1

def counter():
    return rx.hstack(
        rdxt.button(
            "Decrement",
            color_scheme="red",
            on_click=CountState.decrement,
        ),
        rdxt.heading(
            CountState.count,
            font_size="2em",
            padding_x="0.5em",
        ),
        rdxt.button(
            "Increment",
            color_scheme="grass",
            on_click=CountState.increment,
        ),
    )

```

