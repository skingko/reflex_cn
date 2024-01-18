---
components:
    - rx.chakra.RadioGroup
    - rx.chakra.Radio
---

```python exec
import reflex as rx
```

# 单选框

单选框在一系列选项中只允许选择一个选项时使用。

```python demo exec
from typing import List
options: List[str] = ["Option 1", "Option 2", "Option 3"]

class RadioState(rx.State):
    text: str = "No Selection"


def basic_radio_example():
    return rx.vstack(
        rx.badge(RadioState.text, color_scheme="green"),
        rx.radio_group(
            options,
            on_change=RadioState.set_text,
        ),
    )
```

可以使用`default_value`和`default_checked`参数来设置单选框组的默认值。

```python demo
rx.vstack(
    rx.radio_group(
        options,
        default_value="Option 2",
        default_checked=True,
    ),
)
```

可以使用带有`spacing`参数的`hstack`来设置单选框之间的间距。

```python demo
rx.radio_group(
    rx.radio_group(
        rx.hstack(
            rx.foreach(
                options,
                lambda option: rx.radio(option),
            ),
        spacing="2em",
        ),
    ),
)
```

可以使用`vstack`来将单选框垂直堆叠。

```python demo
rx.radio_group(
    rx.radio_group(
        rx.vstack(
            rx.foreach(
                options,
                lambda option: rx.radio(option),
            ),
        ),
    ),
)
```

