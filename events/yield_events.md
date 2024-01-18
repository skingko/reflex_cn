```Chinese
```python exec
import reflex as rx

```

# 发送多个更新

普通的事件处理程序在运行结束后会发送一个`StateUpdate`。这在处理基本事件时很好用，但有时我们需要更复杂的逻辑。为了在事件处理程序中多次更新UI，我们可以使用`yield`来发送更新。

为了达到这个目的，我们可以使用Python关键字`yield`。对于函数内的每个`yield`，一个`StateUpdate`将会被发送到前端，包含到目前为止在事件处理程序执行过程中的变化。

```python demo exec

import asyncio

class MultiUpdateState(rx.State):
    count: int = 0

    async def timed_update(self):
        for i in range(5):
            await asyncio.sleep(0.5)
            self.count += 1
            yield


def multi_update():
    return rx.vstack(
    rx.text(MultiUpdateState.count),
    rx.button("Start", on_click=MultiUpdateState.timed_update)
)

```

下面是使用loading图标来示例多次发送更新的另一个例子。

```python demo exec

import asyncio

class ProgressExampleState(rx.State):
    count: int = 0
    show_progress: bool = False

    async def increment(self):
        self.show_progress = True
        yield
        # Think really hard.
        await asyncio.sleep(0.5)
        self.count += 1
        self.show_progress = False

def progress_example():
    return rx.cond(
        ProgressExampleState.show_progress,
        rx.circular_progress(is_indeterminate=True),
        rx.heading(
            ProgressExampleState.count,
            on_click=ProgressExampleState.increment,
            _hover={"cursor": "pointer"},
        )
    )

```
```

