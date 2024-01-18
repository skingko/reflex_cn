---
components:
    - rx.radix.themes.RadioGroupRoot
    - rx.radix.themes.RadioGroupItem
---


```python exec
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
from pcweb.templates.docpage import style_grid
```



# 单选按钮组

一组可交互的单选按钮，每次只能选择一个。


## 基本示例

```python demo
radio_group_root(
    radio_group_item(value="1"),
    radio_group_item(value="2"),
    radio_group_item(value="3"),
    default_value="1",
)

```

`radio_group_root` 包含了单选按钮组的所有部分。`radio_group_item` 是组内可以被选中的项目。



## 单选按钮组根组件


### 控制数值
使用受控制的 `value` 来确定要选中的单选按钮项。应与 `on_value_change` 事件处理函数一起使用。

```python demo exec
class RadioState1(rx.State):
    text: str = "No Selection"


def radio_state_example():
    return rx.vstack(
        rx.badge(RadioState1.text, color_scheme="green"),
        radio_group_root(
            radio_group_item(value="1"),
            radio_group_item(value="2"),
            radio_group_item(value="3"),
            on_value_change=RadioState1.set_text,
        ),
    )
```


`default_value` 属性可以用来设置初始渲染时应该被选中的单选按钮项的值。


当 `disabled` 属性设置为 `True` 时，禁止用户与单选按钮进行交互。

```python demo
flex(
    radio_group_root(
        radio_group_item(value="1"),
        radio_group_item(value="2"),
    ),
    radio_group_root(
        radio_group_item(value="1"),
        radio_group_item(value="2"),
        disabled=True,
    ),
    gap="2",
)

```


### 使用单选按钮组提交表单

`name` 属性用于给组命名，它会在所属表单中作为名称/值对一起提交。

当 `required` 属性为 `True` 时，表示用户必须在提交所属表单前选择一个单选按钮项。

```python demo exec
class FormRadioState(rx.State):
    form_data: dict = {}

    def handle_submit(self, form_data: dict):
        """Handle the form submit."""
        self.form_data = form_data


def form_example():
    return rx.vstack(
        rx.form(
            rx.vstack(
                radio_group_root(
                    "Radio Group ",
                    radio_group_item(value="1"),
                    radio_group_item(value="2"),
                    radio_group_item(value="3"),
                    name="radio",
                    required=True,
                ),
                rx.button("Submit", type_="submit"),
            ),
            on_submit=FormRadioState.handle_submit,
            reset_on_submit=True,
        ),
        rx.divider(),
        rx.heading("Results"),
        rx.text(FormRadioState.form_data.to_string()),
    )
```




## 单选按钮项


### value
在提交时与 `radio_group_root` 上的 `name` 一起提交的数据。

### disabled
使用 `disabled` 属性创建一个禁用的单选按钮。当为 `True` 时，禁止用户与这个单选按钮进行交互。这与 `radio_group_root` 使用的 `disabled` 属性不同，后者可以禁用单选按钮组中的所有 `radio_group_item` 组件。

```python demo
flex(
    radio_group_root(
        flex(
            text(
                flex(
                    radio_group_item(value="1"),
                    "Off",
                    gap="2",
                ),
                as_="label",
                size="2",
            ),
            text(
                flex(
                    radio_group_item(value="2"),
                    "On",
                    gap="2",
                ),
                as_="label",
                size="2",
            ),
            direction="column",
            gap="2",
        ),
    ),
    radio_group_root(
        flex(
            text(
                flex(
                    radio_group_item(value="1", disabled=True),
                    "Off",
                    gap="2",
                ),
                as_="label",
                size="2",
                color="gray",
            ),
            text(
                flex(
                    radio_group_item(value="2"),
                    "On",
                    gap="2",
                ),
                as_="label",
                size="2",
                color="gray",
            ),
            direction="column",
            gap="2",
        ),
    ),
    direction="column",
    gap="2",

)
```

### required
当为 `True` 时，表示用户必须在提交所属表单前选中这个 `radio_item_group`。只能在使用单个 `radio_group_item` 时使用。

```python demo exec
class FormRadioState2(rx.State):
    form_data: dict = {}

    def handle_submit(self, form_data: dict):
        """Handle the form submit."""
        self.form_data = form_data


def form_example2():
    return rx.vstack(
        rx.form(
            rx.vstack(
                radio_group_root(
                    radio_group_item(value="1", required=True),
                    name="radio",
                ),
                rx.button("Submit", type_="submit"),
            ),
            on_submit=FormRadioState2.handle_submit,
            reset_on_submit=True,
        ),
        rx.divider(),
        rx.heading("Results"),
        rx.text(FormRadioState2.form_data.to_string()),
    )
```




## 样式

### 大小

```python demo
flex(
    radio_group_root(
        radio_group_item(value="1"),
        size="1",
    ),
    radio_group_root(
        radio_group_item(value="1"),
        size="2",
    ),
    radio_group_root(
        radio_group_item(value="1"),
        size="3",
    ),
    gap="2",
)

```


### 变体

```python demo
flex(
    flex(
        radio_group_root(
            radio_group_item(value="1"),
            radio_group_item(value="2"),
            variant="surface",
            default_value="1",
        ),
        direction="column",
        gap="2",
        as_child=True,
    ),
    flex(
        radio_group_root(
            radio_group_item(value="1"),
            radio_group_item(value="2"),
            variant="classic",
            default_value="1",
        ),
        direction="column",
        gap="2",
        as_child=True,
    ),
    flex(
        radio_group_root(
            radio_group_item(value="1"),
            radio_group_item(value="2"),
            variant="soft",
            default_value="1",
        ),
        direction="column",
        gap="2",
        as_child=True,
    ),
    gap="2",
)
```


### 颜色

```python demo
flex(
    radio_group_root(
        radio_group_item(value="1"),
        color_scheme="indigo",
        default_value="1",
    ),
    radio_group_root(
        radio_group_item(value="1"),
        color_scheme="cyan",
        default_value="1",
    ),
    radio_group_root(
        radio_group_item(value="1"),
        color_scheme="orange",
        default_value="1",
    ),
    radio_group_root(
        radio_group_item(value="1"),
        color_scheme="crimson",
        default_value="1",
    ),
    gap="2"
)
```

### 高对比度

使用 `high_contrast` 属性可以提高与背景的颜色对比度。

```python demo
grid(
    radio_group_root(
        radio_group_item(value="1"),
        color_scheme="cyan",
        default_value="1",
    ),
    radio_group_root(
        radio_group_item(value="1"),
        color_scheme="cyan",
        default_value="1",
        high_contrast=True,
    ),
    radio_group_root(
        radio_group_item(value="1"),
        color_scheme="indigo",
        default_value="1",
    ),
    radio_group_root(
        radio_group_item(value="1"),
        color_scheme="indigo",
        default_value="1",
        high_contrast=True,
    ),
    radio_group_root(
        radio_group_item(value="1"),
        color_scheme="orange",
        default_value="1",
    ),
    radio_group_root(
        radio_group_item(value="1"),
        color_scheme="orange",
        default_value="1",
        high_contrast=True,
    ),
    radio_group_root(
        radio_group_item(value="1"),
        color_scheme="crimson",
        default_value="1",
    ),
    radio_group_root(
        radio_group_item(value="1"),
        color_scheme="crimson",
        default_value="1",
        high_contrast=True,
    ),
    rows="2",
    gap="2",
    display="inline-grid",
    flow="column"
)
```


### 对齐方式

将 `radio_group_item` 组合在 `text` 中将自动将其与文本的第一行居中。

```python demo
flex(
    radio_group_root(
        text(
            flex(
                radio_group_item(value="1"),
                "Default",
                gap="2",
            ),
            size="2",
            as_="label",
        ),
        text(
            flex(
                radio_group_item(value="2"),
                "Compact",
                gap="2",
            ),
            size="2",
            as_="label",
        ),
        default_value="1",
        size="1",
    ),
    radio_group_root(
        text(
            flex(
                radio_group_item(value="1"),
                "Default",
                gap="2",
            ),
            size="3",
            as_="label",
        ),
        text(
            flex(
                radio_group_item(value="2"),
                "Compact",
                gap="2",
            ),
            size="3",
            as_="label",
        ),
        default_value="1",
        size="2",
    ),
    radio_group_root(
        text(
            flex(
                radio_group_item(value="1"),
                "Default",
                gap="2",
            ),
            size="4",
            as_="label",
        ),
        text(
            flex(
                radio_group_item(value="2"),
                "Compact",
                gap="2",
            ),
            size="4",
            as_="label",
        ),
        default_value="1",
        size="3",
    ),
    gap="3",
    direction="column",
)
```


```python eval
style_grid(component_used=radio_group_root, component_used_str="radiogrouproot", variants=["classic", "surface", "soft"], components_passed=radio_group_item(), disabled=True,)
```




## 实际示例

```python demo
radio_group_root(
    flex(
        text(
            flex(
                radio_group_item(value="1"),
                "Default",
                gap="2",
            ),
            size="2",
            as_="label",
        ),
        text(
            flex(
                radio_group_item(value="2"),
                "Comfortable",
                gap="2",
            ),
            size="2",
            as_="label",
        ),
        text(
            flex(
                radio_group_item(value="3"),
                "Compact",
                gap="2",
            ),
            size="2",
            as_="label",
        ),
        direction="column",
        gap="2",
    ),
    default_value="1",
)
```

