---
components:
    - rx.chakra.Container
---

```python exec
import reflex as rx
```

容器用于将内容的宽度限制在当前断点范围内，同时保持自适应。

```python demo
rx.container(
    rx.box("Example", bg="blue", color="white", width="50%"),
    center_content=True,
    bg="lightblue",
)
```

