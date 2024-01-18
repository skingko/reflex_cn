```python exec
from pcweb.pages.docs.library import library
from pcweb.pages.docs import state, vars
import reflex as rx
```

# 属性

属性（Props）可以修改组件的行为和外观。它们作为关键字参数传递给组件函数。

## 组件属性

每个组件都有其特定的属性。例如，`rx.avatar` 组件有一个名为 `name` 的属性，用于设置头像的名称。

```python demo
rx.avatar(
    name="John Doe"
)
```

查看您所使用的组件的文档，以了解可用的属性。

```md alert success
# Reflex has a wide selection of [built-in components]({library.path}) to get you started quickly {library.path}.
```

## HTML 属性

组件支持许多标准的 HTML 属性作为属性。例如：HTML [id]({"https://www.w3schools.com/html/html_id.asp"}) 属性直接作为 `id` 属性暴露出来。HTML [className]({"https://www.w3schools.com/jsref/prop_html_classname.asp"}) 属性作为 `class_name` 属性暴露出来（请注意使用了 Python 风格的蛇形命名！）。

```python demo
rx.box(
    "Hello World",
    id="box-id",
    class_name=["class-name-1", "class-name-2",],
)
```

## 将属性绑定到状态

Reflex 应用可以有一个 [状态]({state.overview.path})，用于存储在应用程序运行时可以改变的所有变量，以及可以更改这些变量的事件处理程序。

状态可以根据用户的例如点击按钮的输入或者加载页面的事件等来修改。

状态变量可以绑定到组件的属性，以使界面始终反映应用程序的当前状态。

```md alert warning
Optional: Learn all about [State](state.overview.path) first.
```

您可以将属性的值设置为 [状态变量]({vars.base_vars.path})，以便在变量发生更改时更新组件。

尝试点击下面的徽章来更改它的颜色。

```python demo exec
class PropExampleState(rx.State):
    text: str = "Hello World"
    color: str = "red"

    def flip_color(self):
        if self.color == "red":
            self.color = "blue"
        else:
            self.color = "red"


def index():
    return rx.badge(
        PropExampleState.text,
        color_scheme=PropExampleState.color,
        on_click=PropExampleState.flip_color,
        font_size="1.5em",
        _hover={
            "cursor": "pointer",
        }
    )
```

在这个示例中，`color_scheme` 属性已绑定到 `color` 状态变量。

当调用 `flip_color` 事件处理程序时，`color` 变量会被更新，并且 `color_scheme` 属性会相应更新。

