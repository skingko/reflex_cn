---
components:
    - rx.chakra.Editable
    - rx.chakra.EditablePreview
    - rx.chakra.EditableInput
    - rx.chakra.EditableTextarea
---

```python exec
import reflex as rx
```

# 可编辑组件

可编辑组件用于对一些文本进行内联重命名。
当用户点击或将其聚焦时，它会以普通的 UI 文本形式出现，但会转变为一个文本输入框。

```python demo exec
class EditableState(rx.State):
    example_input: str
    example_textarea: str
    example_state: str

    def set_uppertext(self, example_state: str):
        self.example_state = example_state.upper()


def editable_example():
    return rx.editable(
        rx.editable_preview(),
        rx.editable_input(),
        placeholder="An input example...",
        on_submit=EditableState.set_uppertext,
        width="100%",
    )
```

可编辑组件的另一种变体可以使用文本域而不是输入框。

```python demo
rx.editable(
    rx.editable_preview(),
    rx.editable_textarea(),
    placeholder="A textarea example...",
    on_submit=EditableState.set_example_textarea,
    width="100%",
)
```

