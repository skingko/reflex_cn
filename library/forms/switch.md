---
components:
    - rx.radix.themes.Switch
---

```python exec
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
from pcweb.templates.docpage import style_grid
from pcweb.pages.docs import vars
```

# 开关


复选框的替代开关。

## 基本示例

```python demo
text(
    flex(
        switch(default_checked=True),
        "Sync Settings",
        gap="2",
    )
)

```

在这里，我们将 `default_checked` 属性设置为 `True`，这会在初始渲染时设置开关的状态。

## 用法


### 使用开关提交表单

需要将开关的 `name` 作为名称/值对的一部分提交到所属表单中。

当 `required` 属性为 `True` 时，表示用户必须在提交所属表单之前勾选开关。

`value` 属性仅用于表单提交，使用 `checked` 属性来控制开关的状态。

```python demo exec
class FormSwitchState(rx.State):
    form_data: dict = {}

    def handle_submit(self, form_data: dict):
        """Handle the form submit."""
        self.form_data = form_data


def form_switch():
    return rx.vstack(
        rx.form(
            rx.vstack(
                switch(name="s1"),
                switch(name="s2"),
                switch(name="s3", required=True),
                rx.button("Submit", type_="submit"),
                width="100%",
            ),
            on_submit=FormSwitchState.handle_submit,
            reset_on_submit=True,
            width="100%",
        ),
        rx.divider(),
        rx.heading("Results"),
        rx.text(FormSwitchState.form_data.to_string()),
        width="100%",
    )
```



### 控制值

使用 `checked` 属性来控制开关的状态。

当开关的状态发生变化时，会调用事件 `on_checked_change`，并调用 `change_checked` 事件处理程序。

当 `disabled` 属性为 `True` 时，会阻止用户与开关进行交互。

在下面的示例中，即使第三个开关被禁用，我们仍然可以使用 `checked` 属性来更改其是否被选中。


```python demo exec
class SwitchState2(rx.State):

    checked = True

    def change_checked(self, checked: bool):
        """Change the switch checked var."""
        self.checked = checked


def switch_example2():
    return rx.hstack(
        switch(
            checked=SwitchState2.checked,
            on_checked_change=SwitchState2.change_checked,
        ),
        switch(
            checked=~SwitchState2.checked,
            on_checked_change=lambda v: SwitchState2.change_checked(~v),
        ),
        switch(
            checked=SwitchState2.checked,
            on_checked_change=SwitchState2.change_checked,
            disabled=True,
        ),
    )
```

在此示例中，我们使用 `~` 运算符，它用于对一个变量取反。要了解更多，请查看[变量运算符]({vars.var_operations.path})。


## 样式

```python eval
style_grid(component_used=switch, component_used_str="switch", variants=["classic", "surface", "soft"], disabled=True, default_checked=True)
```


## 现实世界示例


```python demo exec
class FormSwitchState2(rx.State):
    form_data: dict = {}

    cookie_types: dict[str, bool] = {}

    def handle_submit(self, form_data: dict):
        """Handle the form submit."""
        self.form_data = form_data

    def update_cookies(self, cookie_type: str, enabled: bool):
        self.cookie_types[cookie_type] = enabled


def form_switch2():
    return rx.vstack(
            dialog_root(
                dialog_trigger(
                    button("View Cookie Settings", size="4", variant="outline")
                ),
                dialog_content(
                    rx.form(
                        dialog_title("Your Cookie Preferences"),
                        dialog_description(
                            "Change your cookie preferences.",
                            size="2",
                            mb="4",
                        ),
                        flex(
                            text(
                                flex(
                                    "Required",
                                    switch(default_checked=True, disabled=True, name="required"),
                                    gap="2",
                                    justify="between",
                                ),
                                as_="div", size="2", mb="1", weight="bold",
                            ),

                            *[flex(
                                text(cookie_type.capitalize(), as_="div", size="2", mb="1", weight="bold"),
                                text(
                                    flex(
                                        rx.cond(
                                            FormSwitchState2.cookie_types[cookie_type],
                                            "Enabled",
                                            "Disabled",
                                        ),
                                        switch(
                                            name=cookie_type, 
                                            checked=FormSwitchState2.cookie_types[cookie_type], 
                                            on_checked_change=lambda checked: FormSwitchState2.update_cookies(cookie_type, checked)),
                                        gap="2",
                                    ),
                                    as_="div", size="2", mb="1", weight="bold",
                                ),
                                direction="row", justify="between",
                            )
                            for cookie_type in ["functional", "performance", "analytics", "advertisement", "others"]],


                            
                            direction="column",
                            gap="3",
                        ),
                        flex(
                            button("Save & Accept", type_="submit"),
                            dialog_close(
                                button("Exit"),
                            ),
                            gap="3",
                            mt="4",
                            justify="end",
                        ),
                        on_submit=FormSwitchState2.handle_submit,
                        reset_on_submit=True,
                        width="100%",
                    ),
                ),
            ),
        rx.divider(),
        rx.heading("Results"),
        rx.text(FormSwitchState2.form_data.to_string()),
        width="100%",
    )
```

