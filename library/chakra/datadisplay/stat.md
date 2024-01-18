---

components:
    - rx.chakra.Stat
    - rx.chakra.StatLabel
    - rx.chakra.StatNumber
    - rx.chakra.StatHelpText
    - rx.chakra.StatArrow
    - rx.chakra.StatGroup
---

```python exec
import reflex as rx
```

# 统计

统计组件是以简洁明了的方式可视化统计数据的好方法。

```python demo
rx.stat(
    rx.stat_label("Example Price"),
    rx.stat_number("$25"),
    rx.stat_help_text("The price of the item."),
)
```

箭头指示的一组统计示例。

```python demo
rx.stat_group(
        rx.stat(
            rx.stat_number("$250"),
            rx.stat_help_text("%50", rx.stat_arrow(type_="increase")),
        ),
        rx.stat(
            rx.stat_number("£100"),
            rx.stat_help_text("%50", rx.stat_arrow(type_="decrease")),
        ),
        width="100%",
)
```

