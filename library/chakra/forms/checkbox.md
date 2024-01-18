---

components:
    - rx.chakra.Checkbox
---

# 复选框

复选框是切换布尔值的常见方式。
复选框组件可以单独使用，也可以作为一组使用。

```python exec
import reflex as rx
```

```python demo
rx.checkbox("Check Me!")
```

复选框可以有不同的大小和样式。

```python demo
rx.hstack(
    rx.checkbox("Example", color_scheme="green", size="sm"),
    rx.checkbox("Example", color_scheme="blue", size="sm"),
    rx.checkbox("Example", color_scheme="yellow", size="md"),
    rx.checkbox("Example", color_scheme="orange", size="md"),
    rx.checkbox("Example", color_scheme="red", size="lg"),
)
```

复选框还可以具有不同的视觉状态。

```python demo
rx.hstack(
    rx.checkbox(
        "Example", color_scheme="green", size="lg", is_invalid=True
    ),
    rx.checkbox(
        "Example", color_scheme="green", size="lg", is_disabled=True
    ),
)
```

可以使用`on_change`属性将复选框连接到状态。

```python demo exec
import reflex as rx


class CheckboxState(rx.State):
    checked: bool = False

    def toggle(self):
        self.checked = not self.checked


def checkbox_state_example():
    return rx.hstack(
        rx.cond(
            CheckboxState.checked,
            rx.text("Checked", color="green"),
            rx.text("Unchecked", color="red"),
        ),
        rx.checkbox(
            "Example",
            on_change=CheckboxState.set_checked,
        )
    )
```

## 复选框组

您可以使用复选框组将复选框分组。

```python demo
rx.checkbox_group(
    rx.checkbox("Example", color_scheme="green"),
    rx.checkbox("Example", color_scheme="blue"),
    rx.checkbox("Example", color_scheme="yellow"),
    rx.checkbox("Example", color_scheme="orange"),
    rx.checkbox("Example", color_scheme="red"),
    space="1em",
)
```

