---
components:
    - rx.chakra.Divider
---

```python exec
import reflex as rx
```

# 分隔线

分隔线是一种快速内置的方法，用于分隔内容的不同部分。

```python demo
rx.vstack(
    rx.text("Example"),
    rx.divider(border_color="black"),
    rx.text("Example"),
    rx.divider(variant="dashed", border_color="black"),
    width="100%",
)
```

如果使用了垂直方向，请确保父组件已经指定了高度。

```python demo
rx.center(
    rx.divider(
        orientation="vertical", 
        border_color = "black"
    ), 
    height = "4em"
)
```

