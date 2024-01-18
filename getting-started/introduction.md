```python exec
import reflex as rx
from pcweb import constants, styles
from pcweb.templates.docpage import doccode
from pcweb.pages.docs import tutorial
from pcweb.pages.docs import getting_started
from pcweb.pages.docs import wrapping_react
from pcweb.pages.docs.library import library
from pcweb.pages.docs import vars
```

<!-- TODO 我们如何一致地更改页面标题？ -->
# 介绍

**Reflex** 是一个开源框架，用于快速构建漂亮、交互式的Web应用程序，纯粹使用Python。

## 目标

```md section
# Pure Python
Use Python for everything. Don't worry about learning a new language.

# Easy to Learn
Build and share your first app in minutes. No web development experience required.

# Full Flexibility
Remain as flexible as traditional web frameworks. Reflex is easy to use, yet allows for advanced use cases.

Build anything from small data science apps to large, multi-page websites. **This entire site was built and deployed with Reflex!**

# Batteries Included
No need to reach for a bunch of different tools. Reflex handles the user interface, server-side logic, and deployment of your app.
```

## 一个例子：让它变得有意义！

在这里，我们将介绍一个简单的计数器应用程序，允许用户递增或递减计数。

<!-- TODO 使用 radix 组件，以便更简洁地进行样式设置，例如通过所有这些属性 -->

```python exec
class CounterExampleState(rx.State):
    count: int = 0

    def increment(self):
        self.count += 1

    def decrement(self):
        self.count -= 1

state_code = """
class State(rx.State):
    count: int = 0

    def increment(self):
        self.count += 1

    def decrement(self):
        self.count -= 1
"""

def index():
    return rx.hstack(
        rx.button(
            "Decrement",
            bg="#fef2f2",
            color="#b91c1c",
            border_radius="lg",
            on_click=CounterExampleState.decrement,
        ),
        rx.heading(CounterExampleState.count, font_size="2em"),
        rx.button(
            "Increment",
            bg="#ecfdf5",
            color="#047857",
            border_radius="lg",
            on_click=CounterExampleState.increment,
        ),
        spacing="1em",
    )

index_code = """
def index():
    return rx.hstack(
        rx.button(
            "Decrement",
            bg="#fef2f2",
            color="#b91c1c",
            border_radius="lg",
            on_click=State.decrement,
        ),
        rx.heading(State.count, font_size="2em"),
        rx.button(
            "Increment",
            bg="#ecfdf5",
            color="#047857",
            border_radius="lg",
            on_click=State.increment,
        ),
        spacing="1em",
    )
"""

counter_code = f"""
import reflex as rx

{state_code}

{index_code}

app = rx.App()
app.add_page(index)
""".strip()
```

```python demo box
index()
```

这是这个例子的完整代码：

```python
{counter_code}
```

## Reflex 应用程序的结构

让我们逐步分解这个例子。

## 导入

```python eval
doccode(counter_code, lines=(0, 1))
```

我们首先导入 `reflex` 包（别名为 `rx`）。按照惯例，我们将 Reflex 对象引用为 `rx.*`。

## 状态

```python eval
doccode(counter_code, lines=(2, 5))
```

状态定义了应用程序中可以更改的所有变量（称为**[vars]({vars.base_vars.path})**），以及更改它们的函数（称为**[event_handlers](#event-handlers)**）。

在我们的状态中，有一个名为 `count` 的变量，它保存计数器的当前值。我们将其初始化为 `0`。

## 事件处理器

```python eval
doccode(counter_code, lines=(5, 13))
```

在状态中，我们定义了称为**事件处理器**的函数，用于更改状态变量。

事件处理器是 Reflex 中唯一可以修改状态的方法。它们可以作为响应用户操作而调用，例如点击按钮或在文本框中键入文字。这些操作称为**事件**。

我们的计数器应用程序有两个事件处理器，`increment` 和 `decrement`。

## 用户界面（UI）

```python eval
doccode(counter_code, lines=(13, 33))
```

这个函数定义了应用程序的用户界面。

我们使用不同的组件，例如 `rx.hstack`、`rx.button` 和 `rx.heading` 来构建前端。组件可以嵌套创建复杂的布局，并可以使用CSS的全部功能进行样式设置。

Reflex 提供了[50多个内置组件]({library.path})，帮助您入门。我们还在持续添加更多组件。此外，您可以轻松地[封装自己的 React 组件]({wrapping_react.overview.path})。

```python eval
doccode(counter_code, lines=(22, 23))
```

组件可以引用应用程序的状态变量。`rx.heading` 组件通过引用 `State.count` 来显示计数器的当前值。所有引用状态的组件在状态发生变化时都会进行反应性更新。

```python eval
doccode(counter_code, lines=(15, 22))
```

组件通过将事件触发器绑定到事件处理器与状态进行交互。例如，`on_click` 是在用户点击组件时触发的事件。

我们应用程序中的第一个按钮将其 `on_click` 事件绑定到 `State.decrement` 事件处理器上。类似地，第二个按钮将 `on_click` 绑定到 `State.increment`。

换句话说，操作顺序如下：
* 用户在UI上点击“增加”。
* `on_click` 事件被触发。
* 调用事件处理器 `State.increment`。
* `State.count` 增加。
* UI更新以反映 `State.count` 的新值。

## 添加页面

接下来，我们定义应用程序并将计数器组件添加到基本路由。
```python
app = rx.App()
app.add_page(index)
```

## 下一步

🎉 就是这样了！

我们已经使用纯Python创建了一个简单但完全交互式的Web应用程序。

继续阅读我们的文档，您将学会如何使用 Reflex 构建令人惊叹的应用程序。

要了解更多可能性，请查看以下资源：

* 对于一个更实际的示例，请参阅[教程]({tutorial.intro.path})。
* [演示](https://demo.reflex.run)展示了 Reflex 更多的能力。

