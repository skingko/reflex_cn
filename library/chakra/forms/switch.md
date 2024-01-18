将以下内容翻译成中文：

---
components:
    - rx.chakra.Switch
---

```python exec
import reflex as rx
```

# 开关

开关组件可用作复选框组件的替代品。
您可以在已启用和禁用状态之间切换。

```python demo exec
class SwitchState1(rx.State):
    checked: bool = False
    is_checked: bool = "Switch off!"

    def change_check(self, checked: bool):
        self.checked = checked
        if self.checked:
            self.is_checked = "Switch on!"
        else:
            self.is_checked = "Switch off!"


def switch_example():
    return rx.vstack(
        rx.heading(SwitchState1.is_checked),
        rx.switch(
            is_checked=SwitchState1.checked, on_change=SwitchState1.change_check
        ),
    )
```

您还可以通过传递`color_scheme`参数来更改开关组件的颜色方案。
默认颜色方案是蓝色。

```python demo
rx.hstack(
    rx.switch(color_scheme="red"),
    rx.switch(color_scheme="green"),
    rx.switch(color_scheme="yellow"),
    rx.switch(color_scheme="blue"),
    rx.switch(color_scheme="purple"),
)
```

