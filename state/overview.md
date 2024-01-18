```python exec
import reflex as rx
from pcweb.templates.docpage import definition
```

# 状态

状态使我们能够创建可以响应用户输入的交互式应用程序。
它定义了可以随时间变化的变量，以及可以修改它们的函数。

## 状态基础知识

您可以通过创建一个继承自`rx.State`的类来定义状态：

```python
import reflex as rx


class State(rx.State):
    """Define your app state here."""
```

状态类由两个部分组成：变量和事件处理程序。

**变量**是应用程序中可以随时间变化的变量。

**事件处理程序**是响应事件而修改这些变量的函数。

这些是理解 Reflex 中状态工作原理的主要概念：

```python eval
rx.responsive_grid(
    definition(
        "Base Var",
        rx.unordered_list(
            rx.list_item("Any variable in your app that can change over time."),
            rx.list_item(
                "Defined as a field in a ", rx.code("State"), " class"
            ),
            rx.list_item("Can only be modified by event handlers."),
        ),
    ),
    definition(
        "Computed Var",
        rx.unordered_list(
            rx.list_item("Vars that change automatically based on other vars."),
            rx.list_item(
                "Defined as functions using the ",
                rx.code("@rx.var"),
                " decorator.",
            ),
            rx.list_item(
                "Cannot be set by event handlers, are always recomputed when the state changes."
            ),
        ),
    ),
    definition(
        "Event Trigger",
        rx.unordered_list(
            rx.list_item(
                "A user interaction that triggers an event, such as a button click."
            ),
            rx.list_item(
                "Defined as special component props, such as ",
                rx.code("on_click"),
                ".",
            ),
            rx.list_item("Can be used to trigger event handlers."),
        ),
    ),
    definition(
        "Event Handlers",
        rx.unordered_list(
            rx.list_item(
                "Functions that update the state in response to events."
            ),
            rx.list_item(
                "Defined as methods in the ", rx.code("State"), " class."
            ),
            rx.list_item(
                "Can be called by event triggers, or by other event handlers."
            ),
        ),
    ),
    margin_bottom="1em",
    spacing="1em",
    columns=[1, 1, 2, 2, 2],
)
```

## 示例

这是一个在 Reflex 应用程序中使用状态的示例。
单击文本以更改其颜色。

```python demo exec
class ExampleState(rx.State):

    # A base var for the list of colors to cycle through.
    colors: list[str] = ["black", "red", "green", "blue", "purple"]

    # A base var for the index of the current color.
    index: int = 0

    def next_color(self):
        """An event handler to go to the next color."""
        # Event handlers can modify the base vars.
        # Here we reference the base vars `colors` and `index`.
        self.index = (self.index + 1) % len(self.colors)

    @rx.var
    def color(self)-> str:
        """A computed var that returns the current color."""
        # Computed vars update automatically when the state changes.
        return self.colors[self.index]


def index():
    return rx.heading(
        "Welcome to Reflex!",
        # Event handlers can be bound to event triggers.
        on_click=ExampleState.next_color,
        # State vars can be bound to component props.
        color=ExampleState.color,
        _hover={"cursor": "pointer"},
    )
```

基本变量是 `colors` 和 `index`。它们是应用程序中仅可直接在事件处理程序中修改的变量。

有一个计算变量 `color`，它是基本变量的一个函数。每当基本变量发生变化时，它将自动计算。

标题组件将其 `on_click` 事件链接到`ExampleState.next_color` 事件处理程序，该处理程序递增颜色索引。

```md alert success
# With Reflex, you never have to write an API.
All interactions between the frontend and backend are handled through events. 
```

## 客户端状态

每个打开您的应用程序的用户都有唯一的ID和自己的状态副本。
这意味着每个用户可以独立于其他用户与应用程序交互并修改状态。

```md alert
Try opening an app in multiple tabs to see how the state changes independently.
```

所有用户状态存储在服务器上，并且所有事件处理程序在服务器上执行。 Reflex 使用Websockets将事件发送到服务器，并将状态更新发送回客户端。

