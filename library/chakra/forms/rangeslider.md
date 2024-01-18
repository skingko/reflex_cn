---

components:
    - rx.chakra.RangeSlider
    - rx.chakra.RangeSliderTrack
    - rx.chakra.RangeSliderFilledTrack
    - rx.chakra.RangeSliderThumb
---

```python exec
import reflex as rx
```

# 范围滑块

范围滑块用于允许用户在一定数值范围内进行选择。

```python demo exec
from typing import List

class RangeSliderState(rx.State):
    value: List[int] = [0, 100]


def range_slider_example():
    return rx.vstack(
        rx.heading(RangeSliderState.value),
        rx.range_slider(
            on_change_end=RangeSliderState.set_value
        ),
        width="100%",
    )
```

如果你想在每次滑块移动时触发状态变化，可以使用 `on_change` 事件处理程序。
出于性能原因，不建议这样做，只应在需要在每次滑块移动时执行事件时使用。

```python demo
rx.vstack(
    rx.heading(RangeSliderState.value),
    rx.range_slider(
        on_change=RangeSliderState.set_value
    ),
    width="100%",
)
```

