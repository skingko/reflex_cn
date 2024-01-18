```python exec
import reflex as rx
from pcweb.pages.docs import components
from pcweb.pages.docs import styling
import tutorial_style as style
```

# 基本前端

让我们从定义聊天应用的前端开始。在 Reflex 中，前端可以分解为独立的、可重用的组件。有关更多信息，请参阅 [组件文档]
({components.props.path})。

## 显示问题和答案

我们将修改 `chatapp/chatapp.py` 文件中的 `index` 函数，以返回一个显示单个问题和答案的组件。

```python demo box
rx.fragment(
    rx.box(
        "What is Reflex?",
        # The user's question is on the right.
        text_align="right",
    ),
    rx.box(
        "A way to build web apps in pure Python!",
        # The answer is on the left.
        text_align="left",
    ),
)
```

```python
# chatapp.py

import reflex as rx


def index() -> rx.Component:
    return rx.container(
        rx.box(
            "What is Reflex?",
            # The user's question is on the right.
            text_align="right",
        ),
        rx.box(
            "A way to build web apps in pure Python!",
            # The answer is on the left.
            text_align="left",
        ),
    )


# Add state and page to the app.
app = rx.App()
app.add_page(index)
```

可以将组件嵌套在彼此内部以创建复杂的布局。在这里，我们创建一个包含问题和答案的两个盒子的父容器。

我们还为组件添加了一些基本样式。组件接受关键字参数，称为 [props]({components.style_props.path})，用于修改组件的外观和功能。我们使用 `text_align` prop 将文本对齐到左侧和右侧。

## 重用组件

现在我们有了一个显示单个问题和答案的组件，我们可以重用它来显示多个问题和答案。我们将该组件移动到一个单独的函数 `question_answer` 中，并从 `index` 函数中调用它。

```python exec
def qa(question: str, answer: str) -> rx.Component:
    return rx.box(
        rx.box(question, text_align="right"),
        rx.box(answer, text_align="left"),
        margin_y="1em",
    )


qa_pairs = [
    ("What is Reflex?", "A way to build web apps in pure Python!"),
    (
        "What can I make with it?",
        "Anything from a simple website to a complex web app!",
    ),
]


def chat() -> rx.Component:
    qa_pairs = [
        ("What is Reflex?", "A way to build web apps in pure Python!"),
        (
            "What can I make with it?",
            "Anything from a simple website to a complex web app!",
        ),
    ]
    return rx.box(*[qa(question, answer) for question, answer in qa_pairs])
```

```python demo box
rx.container(chat())
```

```python
def qa(question: str, answer: str) -> rx.Component:
    return rx.box(
        rx.box(question, text_align="right"),
        rx.box(answer, text_align="left"),
        margin_y="1em",
    )


def chat() -> rx.Component:
    qa_pairs = [
        ("What is Reflex?", "A way to build web apps in pure Python!"),
        ("What can I make with it?", "Anything from a simple website to a complex web app!"),
    ]
    return rx.box(*[qa(question, answer) for question, answer in qa_pairs])


def index() -> rx.Component:
    return rx.container(chat())
```

## 聊天输入

现在我们想要用户输入问题的方式。为此，我们将使用 [input]({"/docs/library/forms/input"}) 组件让用户添加文本，使用 [button]({"/docs/library/forms/button"}) 组件提交问题。

```python exec
def action_bar() -> rx.Component:
    return rx.hstack(
        rx.input(placeholder="Ask a question"),
        rx.button("Ask"),
    )
```

```python demo box
rx.container(
    chat(),
    action_bar(),
)
```

```python
def action_bar() -> rx.Component:
    return rx.hstack(
        rx.input(placeholder="Ask a question"),
        rx.button("Ask"),
    )

def index() -> rx.Component:
    return rx.container(
        chat(),
        action_bar(),
    )
```

## 样式

让我们为应用添加一些样式。有关样式的更多信息，请参阅 [样式文档]({styling.overview.path})。为了保持代码的整洁，我们将样式移到一个单独的文件 `chatapp/style.py` 中。

```python
# style.py

# Common styles for questions and answers.
shadow = "rgba(0, 0, 0, 0.15) 0px 2px 8px"
chat_margin = "20%"
message_style = dict(
    padding="1em",
    border_radius="5px",
    margin_y="0.5em",
    box_shadow=shadow,
    max_width="30em",
    display="inline-block",
)

# Set specific styles for questions and answers.
question_style = message_style | dict(bg="#F5EFFE", margin_left=chat_margin)
answer_style = message_style | dict(bg="#DEEAFD", margin_right=chat_margin)

# Styles for the action bar.
input_style = dict(
    border_width="1px", padding="1em", box_shadow=shadow
)
button_style = dict(
    bg="#CEFFEE", box_shadow=shadow
)
```

我们将在 `chatapp.py` 中导入样式，并在组件中使用它们。到目前为止，应用应该是这样的：

```python exec
def qa4(question: str, answer: str) -> rx.Component:
    return rx.box(
        rx.box(rx.text(question, style=style.question_style), text_align="right"),
        rx.box(rx.text(answer, style=style.answer_style), text_align="left"),
        margin_y="1em",
        width="100%",
    )


def chat4() -> rx.Component:
    qa_pairs = [
        ("What is Reflex?", "A way to build web apps in pure Python!"),
        (
            "What can I make with it?",
            "Anything from a simple website to a complex web app!",
        ),
    ]
    return rx.box(*[qa4(question, answer) for question, answer in qa_pairs])


def action_bar4() -> rx.Component:
    return rx.hstack(
        rx.input(placeholder="Ask a question", style=style.input_style),
        rx.button("Ask", style=style.button_style),
    )
```

```python demo box
rx.container(
    chat4(),
    action_bar4(),
)
```

```python
# chatapp.py
import reflex as rx

from chatapp import style


def qa(question: str, answer: str) -> rx.Component:
    return rx.box(
        rx.box(rx.text(question, style=style.question_style), text_align="right"),
        rx.box(rx.text(answer, style=style.answer_style), text_align="left"),
        margin_y="1em",
    )

def chat() -> rx.Component:
    qa_pairs = [
        ("What is Reflex?", "A way to build web apps in pure Python!"),
        ("What can I make with it?", "Anything from a simple website to a complex web app!"),
    ]
    return rx.box(*[qa(question, answer) for question, answer in qa_pairs])


def action_bar() -> rx.Component:
    return rx.hstack(
        rx.input(placeholder="Ask a question", style=style.input_style),
        rx.button("Ask", style=style.button_style),
    )


def index() -> rx.Component:
    return rx.container(
        chat(),
        action_bar(),
    )


app = rx.App()
app.add_page(index)
```

应用看起来不错，但它还不够有用！在下一节中，我们将给应用添加一些功能。

