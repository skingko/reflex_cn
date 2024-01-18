```python exec
import reflex as rx
from tutorial_utils import ChatappState
import tutorial_style as style
from pcweb.pages.docs import hosting
```

# 完整的应用程序

我们将使用OpenAI的API为我们的聊天机器人增加一些智能。

## 使用API

我们需要修改我们的事件处理程序以向API发送请求。

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


def action_bar3() -> rx.Component:
    return rx.hstack(
        rx.input(
            value=ChatappState.question,
            placeholder="Ask a question",
            on_change=ChatappState.set_question,
            style=style.input_style,
        ),
        rx.button("Ask", on_click=ChatappState.answer4, style=style.button_style),
    )
```

```python demo box
rx.container(
    chat1(),
    action_bar3(),
)
```

```python
# state.py
import os
from openai import OpenAI

openai.api_key = os.environ["OPENAI_API_KEY"]

...

def answer(self):
    # Our chatbot has some brains now!
    client = OpenAI()
    session = client.chat.completions.create(
        model="gpt-3.5-turbo",
        messages=[
            \{"role": "user", "content": self.question}
        ],
        stop=None,
        temperature=0.7,
        stream=True,
    )

    # Add to the answer as the chatbot responds.
    answer = ""
    self.chat_history.append((self.question, answer))

    # Clear the question input.
    self.question = ""
    # Yield here to clear the frontend input before continuing.
    yield

    for item in session:
        if hasattr(item.choices[0].delta, "content"):
            if item.choices[0].delta.content is None:
                # presence of 'None' indicates the end of the response
                break
            answer += item.choices[0].delta.content
            self.chat_history[-1] = (self.chat_history[-1][0], answer)
            yield
```

最终，我们的聊天机器人完成了！

## 最终代码

我们在三个文件中编写了所有的代码，你可以在下面找到它们。

```python
# chatapp.py
import reflex as rx

from chatapp import style
from chatapp.state import State


def qa(question: str, answer: str) -> rx.Component:
    return rx.box(
        rx.box(rx.text(question, text_align="right"), style=style.question_style),
        rx.box(rx.text(answer, text_align="left"), style=style.answer_style),
        margin_y="1em",
    )

def chat() -> rx.Component:
    return rx.box(
        rx.foreach(
            State.chat_history,
            lambda messages: qa(messages[0], messages[1])
        )
    )


def action_bar() -> rx.Component:
    return rx.hstack(
        rx.input(
            value=State.question,
            placeholder="Ask a question",
            on_change=State.set_question,
            style=style.input_style,
        ),
        rx.button("Ask", on_click=State.answer, style=style.button_style),
    )


def index() -> rx.Component:
    return rx.container(
        chat(),
        action_bar(),
    )


app = rx.App()
app.add_page(index)
```

```python
# state.py
import reflex as rx
import os
import openai


openai.api_key = os.environ["OPENAI_API_KEY"]

class State(rx.State):

    # The current question being asked.
    question: str

    # Keep track of the chat history as a list of (question, answer) tuples.
    chat_history: list[tuple[str, str]]

    def answer(self):
        # Our chatbot has some brains now!
        client = OpenAI()
        session = client.chat.completions.create(
            model="gpt-3.5-turbo",
            messages=[
                \{"role": "user", "content": self.question}
            ],
            stop=None,
            temperature=0.7,
            stream=True,
        )

        # Add to the answer as the chatbot responds.
        answer = ""
        self.chat_history.append((self.question, answer))

        # Clear the question input.
        self.question = ""
        # Yield here to clear the frontend input before continuing.
        yield

        for item in session:
            if hasattr(item.choices[0].delta, "content"):
                if item.choices[0].delta.content is None:
                    # presence of 'None' indicates the end of the response
                    break
                answer += item.choices[0].delta.content
                self.chat_history[-1] = (self.chat_history[-1][0], answer)
                yield

```

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

## 下一步

恭喜！您已经构建了第一个聊天机器人。从这里开始，您可以阅读其他文档以更详细地了解 Reflex。学习的最佳方式是动手构建一些东西，因此尝试使用此代码作为起点构建自己的应用程序！

## 还有一件事

使用我们的托管服务，您可以在几分钟内通过一个命令部署此应用程序。查看我们的[托管快速入门指南]({hosting.deploy_quick_start.path})。

