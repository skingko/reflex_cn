---
components:
    - rx.radix.themes.Separator
---

```python exec
import reflex.components.radix.themes as rdxt
```

# 分割线

在视觉上或语义上分隔内容。

## 基本示例

```python demo
rdxt.flex(
    rdxt.card("Section 1"),
    rdxt.separator(),
    rdxt.card("Section 2"),
    gap="4",
    direction="column",
    align="center",
)
```

## 大小

`size` prop 控制分割线的长度。使用 `size="4"` 会使分割线填充父容器。设置 CSS 的 `width` 或 `height` prop 为 `"100%"` 也可以实现这个效果，但不论方向如何，`size` 的作用都是相同的。

```python demo
rdxt.flex(
    rdxt.card("Section 1"),
    rdxt.separator(size="4"),
    rdxt.card("Section 2"),
    gap="4",
    direction="column",
)
```

## 方向

将方向 prop 设置为 `vertical` 将使分割线垂直显示。

```python demo
rdxt.flex(
    rdxt.card("Section 1"),
    rdxt.separator(orientation="vertical", size="4"),
    rdxt.card("Section 2"),
    gap="4",
    width="100%",
    height="10vh",
)
```

