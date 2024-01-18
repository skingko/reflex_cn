---
components:
    - rx.chakra.NumberInput
    - rx.chakra.NumberInputField
    - rx.chakra.NumberInputStepper
    - rx.chakra.NumberIncrementStepper
    - rx.chakra.NumberDecrementStepper
---

```python exec
import reflex as rx
```

# 数字输入框

数字输入框组件类似于输入框组件，但它还具有递增或递减数值的控件。

```python demo exec
class NumberInputState(rx.State):
    number: int


def number_input_example():
    return rx.number_input(
        value=NumberInputState.number,
        on_change=NumberInputState.set_number,
    )
```

