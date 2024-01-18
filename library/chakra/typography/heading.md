翻译成中文：

---
components:
    - rx.chakra.Heading
---

```python exec
import reflex as rx
```

# 标题

标题组件接收一个字符串并将其显示为标题。

```python demo
rx.heading("Hello World!")
```

可以使用 `size` 属性来更改大小。

```python demo
rx.vstack(
    rx.heading("Hello World!", size= "sm", color="red"),
    rx.heading("Hello World!", size= "md", color="blue"),
    rx.heading("Hello World!", size= "lg", color="green"),
    rx.heading("Hello World!", size= "xl", color="blue"),
    rx.heading("Hello World!", size= "2xl", color="red"),
    rx.heading("Hello World!", size= "3xl", color="blue"),
    rx.heading("Hello World!", size= "4xl", color="green"),
)
```

还可以使用常规 CSS 样式进行样式化。

```python demo
rx.heading("Hello World!", font_size="2em")
```

