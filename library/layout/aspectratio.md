---

组件：
  - rx.radix.themes.AspectRatio
---

```python exec
import reflex as rx
import reflex.components.radix.themes as rdxt
```

# 纵横比

以所需的比例显示内容。

## 基本示例

设置 `ratio` 属性将调整内容的宽度或高度，使得 `宽度` 除以 `高度` 等于 `ratio`。
对于响应式缩放，将内容的 `宽度` 或 `高度` 设置为 `"100%"`。

```python demo
rdxt.grid(
    rdxt.aspect_ratio(
        rdxt.box(
            "Widescreen 16:9",
            background_color="papayawhip",
            width="100%",
            height="100%",
        ),
        ratio=16 / 9,
    ),
    rdxt.aspect_ratio(
        rdxt.box(
            "Letterbox 4:3",
            background_color="orange",
            width="100%",
            height="100%",
        ),
        ratio=4 / 3,
    ),
    rdxt.aspect_ratio(
        rdxt.box(
            "Square 1:1",
            background_color="green",
            width="100%",
            height="100%",
        ),
        ratio=1,
    ),
    rdxt.aspect_ratio(
        rdxt.box(
            "Portrait 5:7",
            background_color="lime",
            width="100%",
            height="100%",
        ),
        ratio=5 / 7,
    ),
    gap="2",
    width="25%",
)
```

```python eval
rx.alert(
    rx.alert_icon(),
    rdxt.box(
        rx.alert_title(
            "Never set ",
            rx.code("height"),
            " or ",
            rx.code("width"),
            " directly on an ",
            rx.code("aspect_ratio"),
            " component or its contents.",
        ),
        rx.alert_description(
            "Instead, wrap the ",
            rx.code("aspect_ratio"),
            " in a ",
            rx.code("box"),
            " that constrains either the width or the height, then set the content width and height to ",
            rx.code('"100%"'),
            ".",
        ),
    ),
    status="warning",
)
```

```python demo
rdxt.flex(
    *[
        rdxt.box(
            rdxt.aspect_ratio(
                rx.image(src="/logo.jpg", width="100%", height="100%"),
                ratio=ratio,
            ),
            width="20%",
        )
        for ratio in [16 / 9, 3 / 2, 2 / 3, 1]
    ],
    justify="between",
    width="100%",
)
```

