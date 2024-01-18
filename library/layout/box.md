---

components:
  - rx.radix.themes.Box
---

```python exec
import reflex as rx
import reflex.components.radix.themes as rdxt
```

# Box

Box 是一个通用的容器组件，用于包装其他组件。

默认情况下，Box 组件基于 `div` 元素并作为块级元素呈现。它的主要作用是应用样式。

## 常用布局属性

与其他布局组件一样，`Box` 提供了简写属性来设置内边距（`p`）和外边距（`m`），使用 radix 的「1」到「9」的刻度。

```python exec
# Migh Level API
def row(prop, description):
    return rdxt.table_row(
        rdxt.table_row_header_cell(prop),
        rdxt.table_cell(description),
    )
```

```python eval
rdxt.table_root(
    rdxt.table_header(
        rdxt.table_row(
            rdxt.table_column_header_cell("Prop"),
            rdxt.table_column_header_cell("Description"),
        ),
    ),
    rdxt.table_body(
        row("p", "Padding for all sides"),
        row("px", "Horizontal padding"),
        row("py", "Vertical padding"),
        row("pt", "Top padding"),
        row("pb", "Bottom padding"),
        row("pl", "Left padding"),
        row("pr", "Right padding"),
        row("m", "Margin for all sides"),
        row("mx", "Horizontal margin"),
        row("my", "Vertical margin"),
        row("mt", "Top margin"),
        row("mb", "Bottom margin"),
        row("ml", "Left margin"),
        row("mr", "Right margin"),
    ),
)
```

## 基本示例

```python demo
rdxt.box(
    rdxt.box("CSS color", background_color="yellow", border_radius="2px", width="20%", m="1", p="1"),
    rdxt.box("CSS color", background_color="orange", border_radius="5px", width="40%", m="2", p="2"),
    rdxt.box("Radix Color", background_color="var(--tomato-3)", border_radius="5px", width="60%", m="3", p="3"),
    rdxt.box("Radix Color", background_color="var(--plum-3)", border_radius="10px", width="80%", m="4", p="4"),
    rdxt.box("Radix Theme Color", background_color="var(--accent-2)", radius="full", width="100%", m="5", p="5"),
    grow="1",
    text_align="center",
)
```

## 背景

要设置背景 [图像](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_images) 或 [渐变](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_images/Using_CSS_gradients)，请使用 [`background` CSS 属性](https://developer.mozilla.org/en-US/docs/Web/CSS/background)。

```python demo
rdxt.flex(
    rdxt.box(background="linear-gradient(45deg, var(--tomato-9), var(--plum-9))", width="20%", height="100%"),
    rdxt.box(background="linear-gradient(red, yellow, blue, orange)", width="20%", height="100%"),
    rdxt.box(background="radial-gradient(at 0% 30%, red 10px, yellow 30%, #1e90ff 50%)", width="20%", height="100%"),
    rdxt.box(background="center/cover url('/reflex_banner.png')", width="20%", height="100%"),
    gap="2",
    width="100%",
    height="10vh",
)
```

