```python exec
import reflex as rx
```


# 事件链式处理

## 从事件处理程序中调用其他事件处理程序

您可以从事件处理程序中调用其他事件处理程序，以保持代码的模块化。只需使用`self.call_handler`语法来运行另一个事件处理程序。如常，您可以在函数内部使用`yield`来向前端发送增量更新。


```python demo exec
import asyncio

class CallHandlerState(rx.State):
    count: int = 0
    progress: int = 0

    async def run(self):
        # Reset the count.
        self.set_progress(0)
        yield

        # Count to 10 while showing progress.
        for i in range(10):
            # Wait and increment.
            await asyncio.sleep(0.5)
            self.count += 1

            # Update the progress.
            self.set_progress(i + 1)

            # Yield to send the update.
            yield


def call_handler_example():
    return rx.vstack(
        rx.badge(CallHandlerState.count, font_size="1.5em", color_scheme="green"),
        rx.progress(value=CallHandlerState.progress, max_=10, width="100%"),
        rx.button("Run", on_click=CallHandlerState.run),
    )
```

## 从事件处理程序返回事件

到目前为止，我们只看到了由组件触发的事件。然而，事件处理程序也可以返回事件。

在 Reflex 中，事件处理程序是同步运行的，因此一次只能运行一个事件处理程序，并且队列中的事件将被阻塞，直到当前事件处理程序完成。返回事件和调用事件处理程序的区别在于，返回事件将发送事件到前端并解除队列的阻塞。

```md alert
Be sure to use the class name `State` (or any substate) rather than `self` when returning events.
```

尝试在下面的输入框中输入一个整数，然后点击其他位置。


```python demo exec
class CollatzState(rx.State):
    count: int = 0

    def start_collatz(self, count: str):
        """Run the collatz conjecture on the given number."""
        self.count = abs(int(count))
        return CollatzState.run_step

    async def run_step(self):
        """Run a single step of the collatz conjecture."""

        while self.count > 1:
            await asyncio.sleep(0.5)

            if self.count % 2 == 0:
                # If the number is even, divide by 2.
                self.count /= 2
            else:
                # If the number is odd, multiply by 3 and add 1.
                self.count = self.count * 3 + 1
            yield


def collatz_example():
    return rx.vstack(
        rx.badge(CollatzState.count, font_size="1.5em", color_scheme="green"),
        rx.input(on_blur=CollatzState.start_collatz),
    )

```

在此示例中，我们对用户输入的数字运行[Collatz 猜想](https://en.wikipedia.org/wiki/Collatz_conjecture)。

当触发 `on_blur` 事件时，将调用事件处理程序 `start_collatz`。它设置了初始计数，然后调用 `run_step` 方法，该方法会一直运行，直到计数达到 `1`。

