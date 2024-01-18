---
components:
    - rx.chakra.AspectRatio
---

```python exec
import reflex as rx
```

保持被包含在区域内的组件的比例。

```python demo
rx.box(element="iframe", src="https://bit.ly/naruto-sage", border_color="red")
```

```python demo
rx.aspect_ratio(
    rx.box(
        element="iframe",
        src="https://bit.ly/naruto-sage",
        border_color="red"
    ),
    ratio=4/3
)
```

