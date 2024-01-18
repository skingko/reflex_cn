```python exec
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
```

# Callout 样式

## 大小

使用 `size` 属性来控制大小。

```python demo
flex(
    callout_root(
        callout_icon(icon(tag="info_circled")),
        callout_text("You will need admin privileges to install and access this application."),
        size="3",
    ),
    callout_root(
        callout_icon(icon(tag="info_circled")),
        callout_text("You will need admin privileges to install and access this application."),
        size="2",
    ),
    callout_root(
        callout_icon(icon(tag="info_circled")),
        callout_text("You will need admin privileges to install and access this application."),
        size="1",
    ),
    direction="column",
    gap="3",
    align="start",
)
```

## 变体

使用 `variant` 属性来控制视觉样式。默认为 `soft`。

```python demo
flex(
    callout_root(
        callout_icon(icon(tag="info_circled")),
        callout_text("You will need admin privileges to install and access this application."),
        variant="soft",
    ),
    callout_root(
        callout_icon(icon(tag="info_circled")),
        callout_text("You will need admin privileges to install and access this application."),
        variant="surface",
    ),
    callout_root(
        callout_icon(icon(tag="info_circled")),
        callout_text("You will need admin privileges to install and access this application."),
        variant="outline",
    ),
    direction="column",
    gap="3",
)
```

## 颜色

使用 `color_scheme` 属性来指定特定的颜色，忽略全局主题。

```python demo
flex(
    callout_root(
        callout_icon(icon(tag="info_circled")),
        callout_text("You will need admin privileges to install and access this application."),
        color_scheme="blue",
    ),
    callout_root(
        callout_icon(icon(tag="info_circled")),
        callout_text("You will need admin privileges to install and access this application."),
        color_scheme="green",
    ),
    callout_root(
        callout_icon(icon(tag="info_circled")),
        callout_text("You will need admin privileges to install and access this application."),
        color_scheme="red",
    ),
    direction="column",
    gap="3",
)
```

## 高对比度

使用 `high_contrast` 属性来增加额外的对比度。

```python demo
flex(
    callout_root(
        callout_icon(icon(tag="info_circled")),
        callout_text("You will need admin privileges to install and access this application."),
    ),
    callout_root(
        callout_icon(icon(tag="info_circled")),
        callout_text("You will need admin privileges to install and access this application."),
        high_contrast=True,
    ),
    direction="column",
    gap="3",
)
```

