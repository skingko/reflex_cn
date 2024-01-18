---
components:
    - rx.chakra.FormControl
    - rx.chakra.FormLabel
    - rx.chakra.FormErrorMessage
    - rx.chakra.FormHelperText
---

# 表单控件

表单控件为表单输入提供上下文，如填充/聚焦/错误/必填等。

```python exec
import reflex as rx
```

```python demo
rx.form_control(
    rx.form_label("First Name", html_for="email"),
    rx.checkbox("Example"),
    rx.form_helper_text("This is a help text"),
    is_required=True,
)
```

下面的示例展示了当名字长度为3或更短时的表单错误。

```python demo exec
import reflex as rx

class FormErrorState(rx.State):
    name: str

    @rx.var
    def is_error(self) -> bool:
         return len(self.name) <= 3

def form_state_example():
    return rx.vstack(
        rx.form_control(
            rx.input(placeholder="name", on_blur=FormErrorState.set_name),
            rx.cond(
                FormErrorState.is_error,
                rx.form_error_message("Name should be more than four characters"),
                rx.form_helper_text("Enter name"),
            ),
            is_invalid=FormErrorState.is_error,
            is_required=True,
        )
    )
```

