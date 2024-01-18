---

components:
    - rx.chakra.Center
    - rx.chakra.Circle
    - rx.chakra.Square
---

```python exec
import reflex as rx
```

Center, Square, and Circle are components that center its children within itself.

```python demo
rx.center(
    rx.text("Hello World!"),
    border_radius="15px",
    border_width="thick",
    width="50%",
)
```

Below are examples of circle and square.

```python demo
rx.hstack(
    rx.square(
        rx.vstack(rx.text("Square")),
        border_width="thick",
        border_color="purple",
        padding="1em",
    ),
    rx.circle(
        rx.vstack(rx.text("Circle")),
        border_width="thick",
        border_color="orange",
        padding="1em",
    ),
    spacing="2em",
)
```

---


组件:

- rx.chakra.Center
- rx.chakra.Circle
- rx.chakra.Square

```python exec
import reflex as rx
```

Center、Square 和 Circle 是组件，它们可以将其子元素居中。

```python demo
rx.center(
    rx.text("Hello World!"),
    border_radius="15px",
    border_width="thick",
    width="50%",
)
```

下面是 Circle 和 Square 的示例。

```python demo
rx.hstack(
    rx.square(
        rx.vstack(rx.text("Square")),
        border_width="thick",
        border_color="purple",
        padding="1em",
    ),
    rx.circle(
        rx.vstack(rx.text("Circle")),
        border_width="thick",
        border_color="orange",
        padding="1em",
    ),
    spacing="2em",
)
```

