---
components:
    - rx.chakra.Spacer
---

```python exec
import reflex as rx
```

创建一个可调整的空白空间，在 Flex 中用于调整子元素之间的间距。

```python demo
rx.flex(
    rx.center(rx.text("Example"), bg="lightblue"),
    rx.spacer(),
    rx.center(rx.text("Example"), bg="lightgreen"),
    rx.spacer(),
    rx.center(rx.text("Example"), bg="salmon"),
    width="100%",
)
```

