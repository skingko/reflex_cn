---
components:
    - rx.chakra.Badge
---

```python exec
import reflex as rx
```

# 徽章

徽章用于快速识别和突出显示物品的状态。

徽章有3个变体：`solid`（实色）、`subtle`（淡色）和`outline`（轮廓）。

```python demo
rx.hstack(
    rx.badge("Example", variant="solid", color_scheme="green"),
    rx.badge("Example", variant="subtle", color_scheme="green"),
    rx.badge("Example", variant="outline", color_scheme="green"),
)
```

配色方案是改变徽章颜色的简便方法。

```python demo
rx.hstack(
    rx.badge("Example", variant="subtle", color_scheme="green"),
    rx.badge("Example", variant="subtle", color_scheme="red"),
    rx.badge("Example", variant="subtle", color_scheme="yellow"),
)
```

您还可以通过传统的样式参数来自定义徽章。

```python demo
rx.badge(
    "Custom Badge", 
    bg="#90EE90",
    color="#3B7A57",
    border_color="#29AB87",
    border_width=2
)
```

