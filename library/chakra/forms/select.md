---

components:
    - rx.chakra.Select
---

```python exec
import reflex as rx
```

# 选择

选择组件用于创建一个选项列表，用户可以从中选择一个或多个选项。

```python demo exec
from typing import List
options: List[str] = ["Option 1", "Option 2", "Option 3"]

class SelectState(rx.State):
    option: str = "No selection yet."


def basic_select_example():
    return rx.vstack(
        rx.heading(SelectState.option),
        rx.select(
            options,
            placeholder="Select an example.",
            on_change=SelectState.set_option,
            color_schemes="twitter",
        ),
    )
```

选择组件还可以同时选择多个选项。

```python demo exec
from typing import List
options: List[str] = ["Option 1", "Option 2", "Option 3"]

class MultiSelectState(rx.State):
    option: List[str] = []


def multiselect_example():
    return rx.vstack(
        rx.heading(MultiSelectState.option),
        rx.select(
            options, 
            placeholder="Select examples", 
            is_multi=True,
            on_change=MultiSelectState.set_option,
            close_menu_on_select=False,
            color_schemes="twitter",
        ),
    )
```

该组件还可以根据需要进行自定义和样式设置，见下面的示例。

```python demo
rx.vstack(
    rx.select(options, placeholder="Select an example.", size="xs"),
    rx.select(options, placeholder="Select an example.", size="sm"),
    rx.select(options, placeholder="Select an example.", size="md"),
    rx.select(options, placeholder="Select an example.", size="lg"),
)
```

```python demo
rx.vstack(
    rx.select(options, placeholder="Select an example.", variant="outline"),
    rx.select(options, placeholder="Select an example.", variant="filled"),
    rx.select(options, placeholder="Select an example.", variant="flushed"),
    rx.select(options, placeholder="Select an example.", variant="unstyled"),
)
```

```python demo
rx.select(
    options,
    placeholder="Select an example.",
    color="white",
    bg="#68D391",
    border_color="#38A169",
)
```

