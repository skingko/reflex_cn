---
components:
    - rx.chakra.Input
---

```python exec
import reflex as rx
```

# 输入框

输入框组件用于接收用户的文本输入。

```python demo exec
class InputState(rx.State):
    text: str = "Type something..."

def basic_input_example():
    return rx.vstack(
        rx.text(InputState.text, color_scheme="green"),
        rx.input(value=InputState.text, on_change=InputState.set_text)
    )
```

"在背后，输入框组件使用了防抖动输入来避免在用户输入过程中向后端发送每个字符的单独状态更新。
这样，状态变量可以直接控制来自后端的 `value` 属性，而用户不会感受到输入延迟。
对于高级用例，您可以通过设置输入框组件的 `debounce_timeout` 来调整防抖动延迟。
您可以在[防抖动输入](/docs/library/forms/debounceinput)组件中找到它的使用示例。"


```python demo exec
class ClearInputState(rx.State):
    text: str

    def clear_text(self):
        self.text = ""


def clear_input_example():
    return rx.vstack(
        rx.text(ClearInputState.text),
        rx.input(
            on_change=ClearInputState.set_text,
            value=ClearInputState.text,
        ),
        rx.button("Clear", on_click=ClearInputState.clear_text),
    )
```

输入框组件还可以使用 `on_blur` 事件处理程序，只有当用户点击输入框外部时才更改状态。
出于性能原因，这样做非常有用，因为只有在用户完成输入时才会更新状态。

```python demo exec
class InputBlurState(rx.State):
    text: str = "Type something..."

    def set_text(self, text: str):
        self.text = text.upper()


def input_blur_example():
    return rx.vstack(
        rx.text(InputBlurState.text),
        rx.input(placeholder="Type something...", on_blur=InputBlurState.set_text)
    )
```

您可以通过使用 `type_` 属性来更改输入框的类型。
例如，您可以创建一个密码输入框或日期选择器。

```python demo
rx.vstack(
    rx.input(type_="password"),
    rx.input(type_="date"),
)
```

我们还提供了 `rx.password` 组件，作为密码输入框的简写形式。

```python demo
rx.password()
```

您还可以将表单与输入框结合使用。
这对于使用单个事件处理程序来收集多个值，并自动支持桌面用户期望的 `Enter` 键提交功能非常有用。

```python demo exec
 class InputFormState(rx.State):

    form_data: dict = \{}

    def handle_submit(self, form_data: dict):
        \"""Handle the form submit.\"""
        self.form_data = form_data
        return [rx.set_value(field_id, "") for field_id in form_data]


def input_form_example():
    return rx.vstack(
        rx.form(
            rx.vstack(
                rx.input(placeholder="First Name", id="first_name"),
                rx.input(placeholder="Last Name", id="last_name"),
                rx.button("Submit", type_="submit"),
            ),
            on_submit=InputFormState.handle_submit,
        ),
        rx.divider(),
        rx.heading("Results"),
        rx.text(InputFormState.form_data.to_string()),
    )
 ```

