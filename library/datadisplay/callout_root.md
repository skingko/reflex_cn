---

components:
    - rx.radix.themes.CalloutRoot
    - rx.radix.themes.CalloutIcon
    - rx.radix.themes.CalloutText
---

```python exec
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
```

# Callout

`Callout`是一条短信息，用于吸引用户的注意力。

```python demo
callout_root(
    callout_icon(icon(tag="info_circled")),
    callout_text("You will need admin privileges to install and access this application."),
)
```

`Callout`组件由`callout_root`组成，它将`callout_icon`和`callout_text`部分组合在一起。该组件基于`div`元素，并支持常见的边距属性。

`callout_icon`提供了与`callout`相关联的`icon`的宽度和高度。该组件基于`div`元素。

!!! 在此处添加一个链接，链接到可以使用的所有不同图标定义的页面 !!!

`callout_text`渲染了Callout的文本。该组件基于`p`元素。

## 作为警告

```python demo
callout_root(
    callout_icon(icon(tag="exclamation_triangle")),
    callout_text("Access denied. Please contact the network administrator to view this page."),
    color_scheme="red",
    role="alert",
)
```

## 样式

### 大小

使用`size`属性控制大小。

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

### 变体

使用`variant`属性来控制视觉样式。默认值为`soft`。

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

### 颜色

使用`color_scheme`属性来指定特定的颜色，忽略全局主题。

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

### 高对比度

使用`high_contrast`属性来增加额外的对比度。

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

