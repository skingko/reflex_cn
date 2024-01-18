---
components:
    - rx.chakra.ResponsiveGrid
---

```python exec
import reflex as rx
```

ResponsiveGrid提供了一个友好的界面，使得创建响应式网格布局变得轻松。SimpleGrid将Box组合在一起，所以您可以传递所有的Box属性和css网格属性以及下面的属性。

为网格布局指定一个固定的列数。

```python demo
rx.responsive_grid(
    rx.box(height="5em", width="5em", bg="lightgreen"),
    rx.box(height="5em", width="5em", bg="lightblue"),
    rx.box(height="5em", width="5em", bg="purple"),
    rx.box(height="5em", width="5em", bg="tomato"),
    rx.box(height="5em", width="5em", bg="orange"),
    rx.box(height="5em", width="5em", bg="yellow"),
    columns=[3],
    spacing="4",
)
```


```python demo
rx.responsive_grid(
    rx.box(height="5em", width="5em", bg="lightgreen"),
    rx.box(height="5em", width="5em", bg="lightblue"),
    rx.box(height="5em", width="5em", bg="purple"),
    rx.box(height="5em", width="5em", bg="tomato"),
    rx.box(height="5em", width="5em", bg="orange"),
    rx.box(height="5em", width="5em", bg="yellow"),
    columns=[1, 2, 3, 4, 5, 6],
)
```

