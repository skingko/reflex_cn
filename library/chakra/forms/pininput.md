---
components:
    - rx.chakra.PinInput
---

```python exec
import reflex as rx
```

# PinInput 锁码输入框

PinInput 锁码输入框与 Input 输入框类似，但它专为输入数字序列进行了优化。

```python demo exec
class PinInputState(rx.State):
    pin: str


def basic_pininput_example():
    return rx.vstack(
        rx.heading(PinInputState.pin),
        rx.box(
            rx.pin_input(
                length=4,
                on_change=PinInputState.set_pin,
                mask=True,
            ),
        ),
    )
```

PinInput 锁码输入框也可以根据下面的示例进行自定义。

```python demo
rx.center(
    rx.pin_input(
        rx.pin_input_field(color="red"),
        rx.pin_input_field(border_color="green"),
        rx.pin_input_field(shadow="md"),
        rx.pin_input_field(color="blue"),
        rx.pin_input_field(border_radius="md"),
        on_change=PinInputState.set_pin,
    )
)
```

