---
components:
    - rx.radix.themes.Heading
---

```python exec
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
```

# 标题

```python demo
heading("The quick brown fox jumps over the lazy dog.")
```

## 作为另一个元素

使用`as_`属性来改变标题的级别。该属性仅具有语义性，并不改变视觉效果。

```python demo
flex(
    heading("Level 1", as_="h1"),
    heading("Level 2", as_="h2"),
    heading("Level 3", as_="h3"),
    direction="column",
    gap="3",
)             
```

## 大小

使用`size`属性来控制标题的大小。该属性还提供正确的行高和修正的字距 - 随着文本大小的增加，相对行高和字距会减小。


```python demo
flex(
    heading("The quick brown fox jumps over the lazy dog.", size="1"),
    heading("The quick brown fox jumps over the lazy dog.", size="2"),
    heading("The quick brown fox jumps over the lazy dog.", size="3"),
    heading("The quick brown fox jumps over the lazy dog.", size="4"),
    heading("The quick brown fox jumps over the lazy dog.", size="5"),
    heading("The quick brown fox jumps over the lazy dog.", size="6"),
    heading("The quick brown fox jumps over the lazy dog.", size="7"),
    heading("The quick brown fox jumps over the lazy dog.", size="8"),
    heading("The quick brown fox jumps over the lazy dog.", size="9"),
    direction="column",
    gap="3",
)
```



## 粗细

使用`weight`属性来设置文本的粗细。

```python demo
flex(
    heading("The quick brown fox jumps over the lazy dog.", weight="light"),
    heading("The quick brown fox jumps over the lazy dog.", weight="regular"),
    heading("The quick brown fox jumps over the lazy dog.", weight="medium"),
    heading("The quick brown fox jumps over the lazy dog.", weight="bold"),
    direction="column",
    gap="3",
)
```


## 对齐

使用`align`属性来设定文本的对齐方式。


```python demo
flex(
    heading("Left-aligned", align="left"),
    heading("Center-aligned", align="center"),
    heading("Right-aligned", align="right"),
    direction="column",
    gap="3",
    width="100%",
)
```


## 修剪

使用`trim`属性来修剪文本开头、结尾或两侧的空格。


```python demo
flex(
    heading("Without Trim",
        trim="normal",
        style={"background": "var(--gray-a2)",
                "border_top": "1px dashed var(--gray-a7)",
                "border_bottom": "1px dashed var(--gray-a7)",}
    ),
    heading("With Trim",
        trim="both",
        style={"background": "var(--gray-a2)",
                "border_top": "1px dashed var(--gray-a7)",
                "border_bottom": "1px dashed var(--gray-a7)",}
    ),
    direction="column",
    gap="3",
)
```


在卡片或其他“盒状”组件中调整垂直间距时，修剪开头空格非常有用。否则，在上下两侧的填充看起来比在两侧要大。

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

使用`color_scheme`属性来分配特定的颜色，忽略全局主题。


```python demo
flex(
    heading("The quick brown fox jumps over the lazy dog.", color_scheme="indigo"),
    heading("The quick brown fox jumps over the lazy dog.", color_scheme="cyan"),
    heading("The quick brown fox jumps over the lazy dog.", color_scheme="crimson"),
    heading("The quick brown fox jumps over the lazy dog.", color_scheme="orange"),
    direction="column",
)
```

## 高对比

使用`high_contrast`属性来增加与背景的颜色对比度。


```python demo
flex(
    heading("The quick brown fox jumps over the lazy dog.", color_scheme="indigo", high_contrast=True),
    heading("The quick brown fox jumps over the lazy dog.", color_scheme="cyan", high_contrast=True),
    heading("The quick brown fox jumps over the lazy dog.", color_scheme="crimson", high_contrast=True),
    heading("The quick brown fox jumps over the lazy dog.", color_scheme="orange", high_contrast=True),
    direction="column",
)
```

