---
components:
    - rx.chakra.Card
    - rx.chakra.CardHeader
    - rx.chakra.CardBody
    - rx.chakra.CardFooter
---

```python exec
import reflex as rx
```

Card是一个灵活的组件，用于以清晰简洁的格式组织和显示内容。

```python demo
rx.card(
    rx.text("Body of the Card Component"), 
    header=rx.heading("Header", size="lg"), 
    footer=rx.heading("Footer",size="sm"),
)
```

您可以使用`header=`来传递头部内容，使用`footer=`来传递底部内容。

