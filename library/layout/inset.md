---
components:
    - rx.radix.themes.Inset
---

```python exec
import reflex as rx
import reflex.components.radix.themes as rdxt
```

# 插入

给容器应用了一个负的外边距，使内容能延伸到周围的容器中。

## 基本示例

将插入组件嵌套在卡片内，将会使内容从卡片的边缘一直延伸到边缘。

```python demo
rdxt.card(
    rdxt.inset(
        rx.image(src="/reflex_banner.png", width="100%", height="auto"),
        side="top",
        pb="current",
    ),
    rdxt.text("Reflex is a web framework that allows developers to build their app in pure Python."),
    width="25vw",
)
```

## 其他方向

`side` 属性控制了负的外边距应用在哪一边。当使用特定的方向时，可以设置相反方向的 padding 为 `current`，以保持与父组件边缘处相同的 padding。

```python demo
rdxt.card(
    rdxt.text("The inset below uses a bottom side."),
    rdxt.inset(
        rx.image(src="/reflex_banner.png", width="100%", height="auto"),
        side="bottom",
        pt="current",
    ),
    width="25vw",
)
```

```python demo
rdxt.card(
    rdxt.flex(
        rdxt.text("This inset uses a right side, which requires a flex with direction row."),
        rdxt.inset(
            rdxt.box(background="center/cover url('/reflex_banner.png')", height="100%"),
            width="100%",
            side="right",
            pl="current",
        ),
        direction="row",
        width="100%",
    ),
    width="25vw",
)
```

```python demo
rdxt.card(
    rdxt.flex(
        rdxt.inset(
            rdxt.box(background="center/cover url('/reflex_banner.png')", height="100%"),
            width="100%",
            side="left",
            pr="current",
        ),
        rdxt.text("This inset uses a left side, which also requires a flex with direction row."),
        direction="row",
        width="100%",
    ),
    width="25vw",
)
```

