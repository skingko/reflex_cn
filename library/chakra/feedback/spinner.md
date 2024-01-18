---

components:
    - rx.chakra.Spinner
---

```python exec
import reflex as rx
```

# 加载器

加载器提供了一个视觉提示，表示一个事件正在进行中，等待一系列的变化或结果。

```python demo
rx.hstack(
    rx.spinner(color="red", size="xs"),
    rx.spinner(color="orange", size="sm"),
    rx.spinner(color="green", size="md"),
    rx.spinner(color="blue", size="lg"),
    rx.spinner(color="purple", size="xl"),
)
```

除了颜色，您还可以使用其他属性（如速度、空颜色和线条粗细）来进一步定制样式。

```python demo
rx.hstack(
    rx.spinner(color="lightgreen", thickness=1, speed="1s", size="xl"),
    rx.spinner(color="lightgreen", thickness=5, speed="1.5s", size="xl"),
    rx.spinner(
        color="lightgreen",
        thickness=10,
        speed="2s",
        empty_color="red",
        size="xl",
    ),
)
```

