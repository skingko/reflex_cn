---

components:
    - rx.chakra.LinkOverlay
---

```python exec
import reflex as rx
```

# LinkOverlay 链接覆盖

Link overlay 提供了一种语义化的方式来在链接中包装元素（卡片，博客文章等）。

```python demo
rx.link_overlay(
    rx.box("Example", bg="black", color="white", font_size=30),
)
```

