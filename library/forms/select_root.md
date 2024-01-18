---
components:
    - rx.radix.themes.SelectRoot
    - rx.radix.themes.SelectTrigger
    - rx.radix.themes.SelectContent
    - rx.radix.themes.SelectGroup
    - rx.radix.themes.SelectItem
    - rx.radix.themes.SelectLabel
    - rx.radix.themes.SelectSeparator
    
---


```python exec
import random
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
from pcweb.templates.docpage import style_grid
```


# 选择

显示一个供用户选择的选项列表，通过按钮触发。


## 基本示例


```python demo
select_root(
    select_trigger(),
    select_content(
        select_group(
            select_label("Fruits"),
            select_item("Orange", value="orange"),
            select_item("Apple", value="apple"),
            select_item("Grape", value="grape", disabled=True),
        ),
        select_separator(),
        select_group(
            select_label("Vegetables"),
            select_item("Carrot", value="carrot"),
            select_item("Potato", value="potato"),
        ),
    ),
    default_value="apple",
)
```


## 用法


## 禁用 


可以使用与`select_item`相关联的`disabled`属性禁用`selet`中的单个项。

```python demo
select_root(
    select_trigger(),
    select_content(
        select_group(
            select_item("Apple", value="apple"),
            select_item("Grape", value="grape", disabled=True),
            select_item("Pineapple", value="pineapple"),
        ),
    ),
)
```

要完全禁用用户与选择交互，请将`select_root`组件的`disabled`属性设置为`True`。

```python demo
select_root(
    select_trigger(),
    select_content(
        select_group(
            select_item("Apple", value="apple"),
            select_item("Grape", value="grape"),
        ),
    ),
    disabled=True,
)
```


## 设置默认值 


在构建`select`时，可以设置多个默认值。

可以在`select_trigger`中设置`placeholder`，这是当未设置值或`default_value`时将呈现的内容。


```python demo
select_root(
    select_trigger(placeholder="pick a fruit"),
    select_content(
        select_group(
            select_item("Apple", value="apple"),
            select_item("Grape", value="grape"),
        ),
    ),
)
```

可以在`select_root`中设置`default_value`，即`select`在初始渲染时的值。


```python demo
select_root(
    select_trigger(),
    select_content(
        select_group(
            select_item("Apple", value="apple"),
            select_item("Grape", value="grape"),
        ),
    ),
    default_value="apple",
)
```



## 对select组件进行高度控制（值和展开状态的变化）


当select的值发生变化时，会调用`on_value_change`事件。在此示例中，我们通过一个按钮来设置`select_root`的`value`属性，从而改变select的值。 

```python demo exec
class SelectState2(rx.State):
    
    values: list[str] = ["apple", "grape", "pear"]
    
    value: str = "apple"

    def change_value(self):
        """Change the select value var."""
        self.value = random.choice(self.values)


def select_example2():
    return rx.vstack(
        select_root(
            select_trigger(),
            select_content(
                select_group(
                    rx.foreach(SelectState2.values, lambda x: select_item(x, value=x))
                ),
            ),
            value=SelectState2.value,
            on_value_change=SelectState2.set_value,
            
        ),
        button("Change Value", on_click=SelectState2.change_value),
        
    )
```



`on_open_change`事件处理程序的工作方式与`on_value_change`类似，在select的展开状态发生变化时调用。

```python demo
select_root(
    select_trigger(),
    select_content(
        select_group(
            select_item("Apple", value="apple"),
            select_item("Grape", value="grape"),
        ),
        
    ),

    on_value_change=rx.window_alert("on_value_change event handler called"),
)

```
 



### 使用select提交表单

作为`select_root`的一个属性，需要为select设置`name`，以便将其作为名称/值对的一部分在表单提交时一起提交。

当`select_root`的`required`属性为`True`时，表示用户必须在提交所属表单之前选择一个值。

`select_item`的`value`属性仅用于表单提交，并在提交时作为数据提供给`name`。使用`value`属性来控制`select`的状态。

```python demo exec
class FormSelectState(rx.State):
    form_data: dict = {}

    def handle_submit(self, form_data: dict):
        """Handle the form submit."""
        self.form_data = form_data


def form_select():
    return rx.vstack(
        rx.form(
            rx.vstack(
                select_root(
                    select_trigger(),
                    select_content(
                        select_group(
                            select_label("Fruits"),
                            select_item("Orange", value="orange"),
                            select_item("Apple", value="apple"),
                            select_item("Grape", value="grape"),
                        ),
                        select_separator(),
                        select_group(
                            select_label("Vegetables"),
                            select_item("Carrot", value="carrot"),
                            select_item("Potato", value="potato"),
                        ),
                    ),
                    default_value="apple",
                    name="select",
                ),
                rx.button("Submit", type_="submit"),
                width="100%",
            ),
            on_submit=FormSelectState.handle_submit,
            reset_on_submit=True,
            width="100%",
        ),
        rx.divider(),
        rx.heading("Results"),
        rx.text(FormSelectState.form_data.to_string()),
        width="100%",
    )
```









## 样式


### 根元素尺寸

### 触发器变体

### 触发器颜色

### 触发器半径


### 内容变体


### 内容颜色

### 内容高对比度


### 内容位置


### 内容侧和侧偏移


### 内容对齐和对齐偏移



## 真实世界示例

```python demo
card(
    rx.vstack(
        rx.image(src="/reflex_logo.png", width="100%", height="auto"),
        flex(
            heading("Reflex Swag", size="4", mb="1"),
            heading("$99", size="6", mb="1"),
            direction="row", justify="between",
            width="100%",
        ),
        text("Reflex swag with a sense of nostalgia, as if they carry whispered tales of past adventures", size="2", mb="1"),
        rx.divider(),
        flex(
            flex(
                text("Color", size="2", mb="1", color_scheme="gray"),
                select_root(
                    select_trigger(),
                    select_content(
                        select_group(
                            select_item("Light", value="light"),
                            select_item("Dark", value="dark"),
                        ),
                    ),
                    default_value="light",
                ),
                direction="column",
            ),
            flex(
                text("Size", size="2", mb="1", color_scheme="gray"),
                select_root(
                    select_trigger(),
                    select_content(
                        select_group(
                            select_item("24", value="24"),
                            select_item("26", value="26"),
                            select_item("28", value="28", disabled=True),
                            select_item("30", value="30"),
                            select_item("32", value="32"),
                            select_item("34", value="34"),
                            select_item("36", value="36"),
                        ),
                    ),
                    default_value="30",
                ),
                direction="column",
            ),
            flex(
                text(".", size="2",),
                button("Add to cart"),
                direction="column",
            ),
            direction="row",
            justify="between",
            width="100%",
        ),
        width="20vw",
    ),
)
```

