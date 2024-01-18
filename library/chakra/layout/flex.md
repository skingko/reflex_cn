---
components:
    - rx.chakra.Flex
---

```python exec
import reflex as rx
```

Flexbox是一种布局模型，可以让元素在容器中对齐和分配空间。利用灵活的宽度和高度，元素可以对齐以填充空间或在元素之间分配空间，这使得它成为响应式设计系统中非常有用的工具。

```python demo
rx.flex(
    rx.center("Center", bg="lightblue"),
    rx.square("Square", bg="lightgreen", padding=10),
    rx.box("Box", bg="salmon", width="150px"),
)
```

将flex与spacer结合使用可以创建可堆叠和响应式的组件。

```python demo
rx.flex(
    rx.center("Center", bg="lightblue"),
    rx.spacer(),
    rx.square("Square", bg="lightgreen", padding=10),
    rx.spacer(),
    rx.box("Box", bg="salmon", width="150px"),
    width = "100%",
)
```

