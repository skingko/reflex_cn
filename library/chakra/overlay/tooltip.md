---

components:
    - rx.chakra.Tooltip
---

```python exec
import reflex as rx
```

# 工具提示

工具提示是在用户与元素交互时出现的简短、信息丰富的消息。
工具提示通常通过鼠标悬停手势或键盘悬停手势来启动。

```python demo
rx.tooltip(
    rx.text("Example", font_size=30),
    label="Tooltip helper.",
)
```

