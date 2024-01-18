---
components:
    - rx.Cond
---

```python exec
import reflex as rx
```

# Cond 条件渲染组件

这个组件用于根据条件渲染其他组件。

Cond 组件接受一个条件和两个组件作为参数。
如果条件为 `True`，则渲染第一个组件，否则渲染第二个组件。

```python demo exec
class CondState(rx.State):
    show: bool = True

    def change(self):
        self.show = not (self.show)


def cond_example():
    return rx.vstack(
        rx.button("Toggle", on_click=CondState.change),
        rx.cond(CondState.show, rx.text("Text 1", color="blue"), rx.text("Text 2", color="red")),
    )
```

第二个组件是可选的，可以省略。
如果省略了第二个组件，并且条件为 `False`，则不会渲染任何内容。

## 否定条件

你可以使用逻辑运算符 `~` 来否定一个条件。

```python
rx.vstack(
    rx.button("Toggle", on_click=CondState.change),
    rx.cond(CondState.show, rx.text("Text 1", color="blue"), rx.text("Text 2", color="red")),
    rx.cond(~CondState.show, rx.text("Text 1", color="blue"), rx.text("Text 2", color="red")),
)
```

## 多重条件

你可以使用逻辑运算符 `&` 和 `|` 来组合多个条件。

```python demo exec
class MultiCondState(rx.State):
    cond1: bool = True
    cond2: bool = False
    cond3: bool = True

    def change(self):
        self.cond1 = not (self.cond1)


def multi_cond_example():
    return rx.vstack(
        rx.button("Toggle", on_click=MultiCondState.change),
        rx.text(
            rx.cond(MultiCondState.cond1, "True", "False"), 
            " & True => ", 
            rx.cond(MultiCondState.cond1 & MultiCondState.cond3, "True", "False"),
        ),
        rx.text(
            rx.cond(MultiCondState.cond1, "True", "False"), 
            " & False => ", 
            rx.cond(MultiCondState.cond1 & MultiCondState.cond2, "True", "False"),
        ),  
        rx.text(
            rx.cond(MultiCondState.cond1, "True", "False"), 
            " | False => ", 
            rx.cond(MultiCondState.cond1 | MultiCondState.cond2, "True", "False"),
        ),
    )
```

