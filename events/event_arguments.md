```python exec
import reflex as rx
```

# 事件参数

在某些情况下，您想要向事件处理程序传递附加参数。为了做到这一点，您可以将事件触发器绑定到一个lambda函数上，该函数可以使用您想要的参数调用事件处理程序。

尝试在下面的输入框中输入一个颜色，并在点击输入框外部时改变输入框的颜色。

```python demo exec
class ArgState(rx.State):
    colors: list[str] = ["rgba(222,44,12)", "white", "#007ac2"]

    def change_color(self, color: str, index: int):
        self.colors[index] = color

def event_arguments_example():
    return rx.hstack(
        rx.input(default_value=ArgState.colors[0], on_blur=lambda c: ArgState.change_color(c, 0), bg=ArgState.colors[0]),
        rx.input(default_value=ArgState.colors[1], on_blur=lambda c: ArgState.change_color(c, 1), bg=ArgState.colors[1]),
        rx.input(default_value=ArgState.colors[2], on_blur=lambda c: ArgState.change_color(c, 2), bg=ArgState.colors[2]),
    )

```

在这个例子中，我们想要将两个参数传递给事件处理程序 `change_color`，即颜色和要更改的颜色的索引。

`on_blur` 事件触发器将输入框的文本作为参数传递给lambda函数，然后lambda函数使用文本和输入框的索引调用 `change_color` 事件处理程序。

```md alert warning
# Event Handler Parameters should provide type annotations.
Like state vars, be sure to provide the right type annotations for the parameters in an event handler.
```

