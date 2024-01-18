---
components:
    - rx.radix.themes.Kbd
---

```python exec
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
```

# Kbd（键盘）

表示键盘输入或热键。

```python demo
kbd("Shift + Tab")
```

## 大小

使用 `size` 属性来控制文本的大小。该属性还提供正确的行高和纠正的字母间距。随着文本大小的增加，相对行高和字母间距减小。

```python demo
flex(
    kbd("Shift + Tab", size="1"),
    kbd("Shift + Tab", size="2"),
    kbd("Shift + Tab", size="3"),
    kbd("Shift + Tab", size="4"),
    kbd("Shift + Tab", size="5"),
    kbd("Shift + Tab", size="6"),
    kbd("Shift + Tab", size="7"),
    kbd("Shift + Tab", size="8"),
    kbd("Shift + Tab", size="9"),
    direction="column",
    gap="3",
)
```

