```Chinese
---

组件:
- rx.radix.themes.Code

---

```python exec
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
```

# 代码

```python demo
code("console.log()")
```

## 字体大小

使用 `size` 属性来控制文本大小。该属性还提供了正确的行高和矫正的字距。随着文字大小的增加，相对行高和字距会减小。

```python demo
flex(
    code("console.log()", size="1"),
    code("console.log()", size="2"),
    code("console.log()", size="3"),
    code("console.log()", size="4"),
    code("console.log()", size="5"),
    code("console.log()", size="6"),
    code("console.log()", size="7"),
    code("console.log()", size="8"),
    code("console.log()", size="9"),
    direction="column",
    gap="3",
    align="start",
)
```

## 字重

使用 `weight` 属性来设置文本的字重。

```python demo
flex(
    code("console.log()", weight="light"),
    code("console.log()", weight="regular"),
    code("console.log()", weight="medium"),
    code("console.log()", weight="bold"),
    direction="column",
    gap="3",
)
```

## 变体

使用 `variant` 属性来控制视觉样式。

```python demo
flex(
    code("console.log()", variant="solid"),
    code("console.log()", variant="soft"),
    code("console.log()", variant="outline"),
    code("console.log()", variant="ghost"),
    direction="column",
    gap="2",
    align="start",
)
```

## 颜色

使用 `color_scheme` 属性来设置特定颜色，忽略全局主题。

```python demo
flex(
    code("console.log()", color_scheme="indigo"),
    code("console.log()", color_scheme="crimson"),
    code("console.log()", color_scheme="orange"),
    code("console.log()", color_scheme="cyan"),
    direction="column",
    gap="2",
    align="start",
)
```

## 高对比度

使用 `high_contrast` 属性来增加与背景的颜色对比度。

```python demo
flex(
    flex(
        code("console.log()", variant="solid"),
        code("console.log()", variant="soft"),
        code("console.log()", variant="outline"),
        code("console.log()", variant="ghost"),
        direction="column",
        align="start",
        gap="2",
    ),
    flex(
        code("console.log()", variant="solid", high_contrast=True),
        code("console.log()", variant="soft", high_contrast=True),
        code("console.log()", variant="outline", high_contrast=True),
        code("console.log()", variant="ghost", high_contrast=True),
        direction="column",
        align="start",
        gap="2",
    ),
    gap="3",
)
```

```

