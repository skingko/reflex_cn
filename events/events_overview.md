```python exec
import reflex as rx

from pcweb.pages.docs.library import library
```

# 事件概述

事件是我们修改状态并使应用程序具有交互性的方式。

事件触发器是创建要发送到事件处理程序的事件的组件属性。
每个组件都支持一组事件触发器。在每个[组件的文档]（{library.path}）中，它们在事件触发器部分进行了描述。

让我们看一个下面的例子。尝试将鼠标悬停在标题上以更改单词。

```python demo exec
class WordCycleState(rx.State):
    # The words to cycle through.
    text: list[str] = ["Welcome", "to", "Reflex", "!"]

    # The index of the current word.
    index: int = 0

    def next_word(self):
        self.index = (self.index + 1) % len(self.text)

    @rx.var
    def get_text(self) -> str:
        return self.text[self.index]

def event_triggers_example():
    return rx.heading(
        WordCycleState.get_text,
        on_mouse_over=WordCycleState.next_word,
        color="green",
    )

```

在这个例子中，标题组件具有事件触发器 `on_mouse_over`。
每当用户在标题上悬停时，将调用 `next_word` 处理程序来循环单词。一旦处理程序返回，用户界面将更新以反映新的状态。

