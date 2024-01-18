---
components:
    - rx.chakra.Wrap
    - rx.chakra.WrapItem
---

```python exec
import reflex as rx
```

Wrap 是一个布局组件，可以在其子组件之间添加定义好的间距。

如果在同一行中没有足够的空间容纳更多的子组件，它会自动换行。可以将其视为具有间距支持的智能 flex-wrap。


```python demo
rx.wrap(
    rx.wrap_item(rx.box("Example", bg="lightgreen", w="100px", h="80px")),
    rx.wrap_item(rx.box("Example", bg="lightblue", w="200px", h="80px")),
    rx.wrap_item(rx.box("Example", bg="red", w="300px", h="80px")),
    rx.wrap_item(rx.box("Example", bg="orange", w="400px", h="80px")),
    width="100%",
    spacing="2em",
    align="center",
)
```

