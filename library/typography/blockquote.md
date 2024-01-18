---
components:
    - rx.radix.themes.Blockquote
---

```python exec
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
```

# 引用块

```python demo
blockquote("Perfect typography is certainly the most elusive of all arts.")
```


## 大小

使用 `size` 属性来控制引用块的大小。该属性还提供了正确的行高和修正的字母间距 - 文本大小增加时，相对行高和字母间距减少。

```python demo
flex(
    blockquote("Perfect typography is certainly the most elusive of all arts.", size="1"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", size="2"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", size="3"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", size="4"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", size="5"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", size="6"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", size="7"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", size="8"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", size="9"),
    direction="column",
    gap="3",
)
```


## 权重

使用 `weight` 属性设置引用块的权重。

```python demo
flex(
    blockquote("Perfect typography is certainly the most elusive of all arts.", weight="light"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", weight="regular"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", weight="medium"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", weight="bold"),
    direction="column",
    gap="3",
)
```


## 颜色

使用 `color_scheme` 属性为引用块分配特定的颜色，忽略全局主题。

```python demo
flex(
    blockquote("Perfect typography is certainly the most elusive of all arts.", color_scheme="indigo"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", color_scheme="cyan"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", color_scheme="crimson"),
    blockquote("Perfect typography is certainly the most elusive of all arts.", color_scheme="orange"),
    direction="column",
    gap="3",
)
```


## 高对比度

使用 `high_contrast` 属性增加与背景的颜色对比度。

```python demo
flex(
    blockquote("Perfect typography is certainly the most elusive of all arts."),
    blockquote("Perfect typography is certainly the most elusive of all arts.", high_contrast=True),
    direction="column",
    gap="3",
)
```

