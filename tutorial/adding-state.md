```python exec
import os

import reflex as rx
import openai

from pcweb.pages.docs import state
from pcweb.pages.docs import events

from tutorial_utils import ChatappState
import tutorial_style as style

# If it's in environment, no need to hardcode (openai SDK will pick it up)
if "OPENAI_API_KEY" not in os.environ:
    openai.api_key = "YOUR_OPENAI_KEY"

```

# 状态

现在让我们通过添加状态使聊天应用程序具有互动性。状态是我们定义应用程序中可以更改的所有变量和可以修改它们的所有函数的位置。您可以在[state docs]({state.overview.path})中了解更多关于状态的信息。

## 定义状态

我们将在`chatapp`目录中创建一个名为`state.py`的新文件。我们的状态将跟踪当前正在提问的问题和聊天历史记录。我们还将定义一个事件处理程序`answer`，它将处理当前问题并将答案添加到聊天历史记录中。

```python
# state.py
import reflex as rx


class State(rx.State):

    # The current question being asked.
    question: str

    # Keep track of the chat history as a list of (question, answer) tuples.
    chat_history: list[tuple[str, str]]

    def answer(self):
        # Our chatbot is not very smart right now...
        answer = "I don't know!"
        self.chat_history.append((self.question, answer))

```

## 将状态绑定到组件

现在我们可以在`chatapp.py`中导入状态并在前端组件中引用它。我们将修改`chat`组件，以使用状态而不是当前的固定问题和答案。

```python exec
def qa(question: str, answer: str) -> rx.Component:
    return rx.box(
        rx.box(rx.text(question, style=style.question_style), text_align="right"),
        rx.box(rx.text(answer, style=style.answer_style), text_align="left"),
        margin_y="1em",
        width="100%",
    )


def chat1() -> rx.Component:
    return rx.box(
        rx.foreach(
            ChatappState.chat_history, lambda messages: qa(messages[0], messages[1])
        )
    )


def action_bar1() -> rx.Component:
    return rx.hstack(
        rx.input(
            placeholder="Ask a question",
            on_change=ChatappState.set_question,
            style=style.input_style,
        ),
        rx.button("Ask", on_click=ChatappState.answer, style=style.button_style),
    )
```

```python demo box
rx.container(
    chat1(),
    action_bar1(),
)
```

```python
# chatapp.py
from chatapp.state import State
...

def chat() -> rx.Component:
    return rx.box(
        rx.foreach(
            State.chat_history,
            lambda messages: qa(messages[0], messages[1])
        )
    )

...

def action_bar() -> rx.Component:
    return rx.hstack(
        rx.input(placeholder="Ask a question", on_change=State.set_question, style=style.input_style),
        rx.button("Ask", on_click=State.answer, style=style.button_style),
    )
```

普通的Python `for`循环不能用于迭代状态变量，因为这些值可以更改，并且在编译时是未知的。相反，我们使用[foreach]({"/docs/library/layout/foreach"})组件来遍历聊天历史记录。

我们还将输入的`on_change`事件绑定到`set_question`事件处理程序，它将在用户输入时更新`question`状态变量。我们将按钮的`on_click`事件绑定到`answer`事件处理程序，它将处理问题并将答案添加到聊天历史记录中。`set_question`事件处理程序是一个内置的隐式定义的事件处理程序。每个基础变量都有一个。在[events docs]({events.setters.path})的Setters部分中了解更多信息。

## 清除输入

当前用户单击按钮后输入框不会清除。我们可以通过将输入的值绑定到`question`来解决此问题，使用`value=State.question`，并在运行`answer`事件处理程序时清除它，使用`self.question = ''`。

```python exec
def action_bar2() -> rx.Component:
    return rx.hstack(
        rx.input(
            value=ChatappState.question,
            placeholder="Ask a question",
            on_change=ChatappState.set_question,
            style=style.input_style,
        ),
        rx.button("Ask", on_click=ChatappState.answer2, style=style.button_style),
    )
```

```python demo box
rx.container(
    chat1(),
    action_bar2(),
)
```

```python
# chatapp.py
def action_bar() -> rx.Component:
    return rx.hstack(
        rx.input(
            value=State.question,
            placeholder="Ask a question",
            on_change=State.set_question,
            style=style.input_style),
        rx.button("Ask", on_click=State.answer, style=style.button_style),
    )

```python
# state.py

def answer(self):
    # Our chatbot is not very smart right now...
    answer = "I don't know!"
    self.chat_history.append((self.question, answer))
    self.question = ""
```
        



## Streaming Text

Normally state updates are sent to the frontend when an event handler returns. However, we want to stream the text from the chatbot as it is generated. We can do this by yielding from the event handler. See the [yield events docs]({events.yield_events.path}) for more info.


```python exec
def action_bar3() -> rx.Component:
    return rx.hstack(
        rx.input(
            value=ChatappState.question,
            placeholder="Ask a question",
            on_change=ChatappState.set_question,
            style=style.input_style,
        ),
        rx.button("Ask", on_click=ChatappState.answer3, style=style.button_style),
    )
```

```python demo box
rx.container(
    chat1(),
    action_bar3(),
)
```

```python
#state.py
import asyncio

...
async def answer(self):
    # Our chatbot is not very smart right now...
    answer = "I don't know!"
    self.chat_history.append((self.question, ""))

    # Clear the question input.
    self.question = ""
    # Yield here to clear the frontend input before continuing.
    yield

    for i in range(len(answer)):
        # Pause to show the streaming effect.
        await asyncio.sleep(0.1)
        # Add one letter at a time to the output.
        self.chat_history[-1] = (self.chat_history[-1][0], answer[:i + 1])
        yield
```

在下一部分中，我们将通过添加人工智能来完成我们的聊天机器人！

