---

components:
    - rx.chakra.Form
---

```python exec
import reflex as rx
```

# 表单

表单用于收集用户输入。组件 `rx.form` 用于将输入字段分组并一起提交。

表单组件的子组件可以是表单控件，例如 `rx.input`、`rx.checkbox` 或 `rx.switch`。这些控件应该有一个 `name` 属性，用于在表单数据中标识控件。当`on_submit` 事件被触发时，表单数据以字典形式提交给 `handle_submit` 事件处理程序。

当用户点击提交按钮或在表单控件上按下回车键时，表单将被提交。

```python demo exec
class FormState(rx.State):
    form_data: dict = {}

    def handle_submit(self, form_data: dict):
        """Handle the form submit."""
        self.form_data = form_data


def form_example():
    return rx.vstack(
        rx.form(
            rx.vstack(
                rx.input(placeholder="First Name", name="first_name"),
                rx.input(placeholder="Last Name", name="last_name"),
                rx.hstack(
                    rx.checkbox("Checked", name="check"),
                    rx.switch("Switched", name="switch"),
                ),
                rx.button("Submit", type_="submit"),
            ),
            on_submit=FormState.handle_submit,
            reset_on_submit=True,
        ),
        rx.divider(),
        rx.heading("Results"),
        rx.text(FormState.form_data.to_string()),
    )
```

```md alert warning
# When using the form you must include a button or input with `type_='submit'`.
```

## 动态表单

可以通过使用 `rx.foreach` 对状态变量进行迭代来动态创建表单。

此示例允许用户在提交之前向表单中添加新的字段，并且所有字段都将包含在传递给 `handle_submit` 函数的表单数据中。

```python demo exec
class DynamicFormState(rx.State):
    form_data: dict = {}
    form_fields: list[str] = ["first_name", "last_name", "email"]

    @rx.cached_var
    def form_field_placeholders(self) -> list[str]:
        return [
            " ".join(w.capitalize() for w in field.split("_"))
            for field in self.form_fields
        ]

    def add_field(self, form_data: dict):
        new_field = form_data.get("new_field")
        if not new_field:
            return
        field_name = new_field.strip().lower().replace(" ", "_")
        self.form_fields.append(field_name)

    def handle_submit(self, form_data: dict):
        self.form_data = form_data


def dynamic_form():
    return rx.vstack(
        rx.form(
            rx.vstack(
                rx.foreach(
                    DynamicFormState.form_fields,
                    lambda field, idx: rx.input(
                        placeholder=DynamicFormState.form_field_placeholders[idx],
                        name=field,
                    ),
                ),
                rx.button("Submit", type_="submit"),
            ),
            on_submit=DynamicFormState.handle_submit,
            reset_on_submit=True,
        ),
        rx.form(
            rx.hstack(
                rx.input(placeholder="New Field", name="new_field"),
                rx.button("+", type_="submit"),
            ),
            on_submit=DynamicFormState.add_field,
            reset_on_submit=True,
        ),
        rx.divider(),
        rx.heading("Results"),
        rx.text(DynamicFormState.form_data.to_string()),
    )
```

