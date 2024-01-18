```yaml
components:
    - rx.radix.themes.Text
```

```python exec
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
```

# 文本

```python demo
text("The quick brown fox jumps over the lazy dog.")
```

## 作为另一个元素

使用 `as_` 属性将文本呈现为 `p`、`label`、`div` 或 `span`。这个属性纯粹是语义化的，不会改变视觉外观。

```python demo
flex(
    text("This is a ", strong("paragraph"), " element.", as_="p"),
    text("This is a ", strong("label"), " element.", as_="label"),
    text("This is a ", strong("div"), " element.", as_="div"),
    text("This is a ", strong("span"), " element.", as_="span"),
    direction="column",
    gap="3",
)             
```

## 大小

使用 `size` 属性来控制文本的大小。该属性还提供了正确的行高和修正的字母间距——随着文本大小的增加，相对行高和字母间距会减小。

```python demo
flex(
    text("The quick brown fox jumps over the lazy dog.", size="1"),
    text("The quick brown fox jumps over the lazy dog.", size="2"),
    text("The quick brown fox jumps over the lazy dog.", size="3"),
    text("The quick brown fox jumps over the lazy dog.", size="4"),
    text("The quick brown fox jumps over the lazy dog.", size="5"),
    text("The quick brown fox jumps over the lazy dog.", size="6"),
    text("The quick brown fox jumps over the lazy dog.", size="7"),
    text("The quick brown fox jumps over the lazy dog.", size="8"),
    text("The quick brown fox jumps over the lazy dog.", size="9"),
    direction="column",
    gap="3",
)
```

2-4号尺寸适用于长篇内容。1-3号尺寸适用于UI标签。

## 粗细

使用 `weight` 属性来设置文本的粗细。

```python demo
flex(
    text("The quick brown fox jumps over the lazy dog.", weight="light", as_="div"),
    text("The quick brown fox jumps over the lazy dog.", weight="regular", as_="div"),
    text("The quick brown fox jumps over the lazy dog.", weight="medium", as_="div"),
    text("The quick brown fox jumps over the lazy dog.", weight="bold", as_="div"),
    direction="column",
    gap="3",
)
```

## 对齐

使用 `align` 属性来设置文本的对齐方式。

```python demo
flex(
    text("Left-aligned", align="left", as_="div"),
    text("Center-aligned", align="center", as_="div"),
    text("Right-aligned", align="right", as_="div"),
    direction="column",
    gap="3",
    width="100%",
)
```

## 裁剪

使用 `trim` 属性来裁剪文本框开头、结尾或两侧的前导空格。

```python demo
flex(
    text("Without Trim",
        trim="normal",
        style={"background": "var(--gray-a2)",
                "border_top": "1px dashed var(--gray-a7)",
                "border_bottom": "1px dashed var(--gray-a7)",}
    ),
    text("With Trim",
        trim="both",
        style={"background": "var(--gray-a2)",
                "border_top": "1px dashed var(--gray-a7)",
                "border_bottom": "1px dashed var(--gray-a7)",}
    ),
    direction="column",
    gap="3",
)
```

在卡片或其他"盒状"组件中调整垂直间距时，裁剪前导空格非常有用。否则，上下的填充看起来比两侧的填充要大。

```python demo
flex(
    box(
        heading("Without trim", mb="1", size="3",),
        text("The goal of typography is to relate font size, line height, and line width in a proportional way that maximizes beauty and makes reading easier and more pleasant."),
        style={"background": "var(--gray-a2)", 
                "border": "1px dashed var(--gray-a7)",},
        p="4",
    ),
    box(
        heading("With trim", mb="1", size="3", trim="start"),
        text("The goal of typography is to relate font size, line height, and line width in a proportional way that maximizes beauty and makes reading easier and more pleasant."),
        style={"background": "var(--gray-a2)", 
                "border": "1px dashed var(--gray-a7)",},
        p="4",
    ),
    direction="column",
    gap="3",
)
```

## 颜色

使用 `color_scheme` 属性来指定特定的颜色，忽略全局主题。

```python demo
flex(
    text("The quick brown fox jumps over the lazy dog.", color_scheme="indigo"),
    text("The quick brown fox jumps over the lazy dog.", color_scheme="cyan"),
    text("The quick brown fox jumps over the lazy dog.", color_scheme="crimson"),
    text("The quick brown fox jumps over the lazy dog.", color_scheme="orange"),
    direction="column",
)
```

## 高对比度

使用 `high_contrast` 属性来增加与背景之间的颜色对比度。

```python demo
flex(
    text("The quick brown fox jumps over the lazy dog.", color_scheme="indigo", high_contrast=True),
    text("The quick brown fox jumps over the lazy dog.", color_scheme="cyan", high_contrast=True),
    text("The quick brown fox jumps over the lazy dog.", color_scheme="crimson", high_contrast=True),
    text("The quick brown fox jumps over the lazy dog.", color_scheme="orange", high_contrast=True),
    direction="column",
)
```

## 带有格式

与格式化组件一起组合 `Text`，以增强内容的强调和结构。

```python demo
text(
    "Look, such a helpful ",
    link("link", href="#"),
    ", an ",
    em("italic emphasis"),
    " a piece of computer ",
    code("code"),
    ", and even a hotkey combination ",
    kbd("⇧⌘A"),
    " within the text.",
    size="5",
)
```

## 带有表单控件

将 `text` 与类似 `checkbox`、`radiogroup` 或 `smart switch` 的表单控件组合时，即使文本是多行的，也会自动将控件居中于第一行文本。

```python demo
box(
    text(
        flex(
            checkbox(default_checked=True),
            "I understand that these documents are confidential and cannot be shared with a third party.",
        ),
        as_="label",
        size="3",
    ),
    style={"max_width": 300},
)
```

