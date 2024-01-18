---
components:
    - rx.radix.themes.CalloutRoot
---

```python exec
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
```

# Callout（提示）

一个吸引用户注意力的简短消息。

下面是使用`callout`组件的简单示例。

```python demo
callout_root(
    callout_icon(icon(tag="info_circled")),
    callout_text("You will need admin privileges to install and access this application."),
)
```

`callout`组件由`callout_root`组成，其中包含了`callout_icon`和`callout_text`两部分。该组件基于`div`元素，并支持常见的外边距属性。

`callout_icon`为与`callout`相关联的图标提供了宽度和高度，该组件基于`div`元素。

!!! 在此添加链接，指向我们定义了所有可用图标的页面 !!!

`callout_text`用于呈现提示的文本内容，该组件基于`p`元素。


## 作为警报

```python demo
callout_root(
    callout_icon(icon(tag="exclamation_triangle")),
    callout_text("Access denied. Please contact the network administrator to view this page."),
    color_scheme="red",
    role="alert",
)
```

