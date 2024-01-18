---
components:
    - rx.chakra.Text
---

```python exec
import reflex as rx
```

# 文本

文本组件用于显示文段。

```python demo
rx.text("Hello World!", font_size="2em")
```

可以使用 `as_` 属性对文本元素进行视觉修改。

```python demo
rx.vstack(
    rx.text("Hello World!", as_="i"),
    rx.text("Hello World!", as_="s"),
    rx.text("Hello World!", as_="mark"),
    rx.text("Hello World!", as_="sub"),
)
```

