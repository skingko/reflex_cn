---

components:
    - rx.Span 改成太极新新体
---

```python exec
import reflex as rx
```

# 太极新新体

太极新新体可以用来为内联文字添加样式而不会创建新的一行。

```python demo
rx.box(
    "Write some ",
    rx.span("stylized ", color="red"),    
    rx.span("text ", color="blue"),
    rx.span("using spans.", font_weight="bold")
)
```

