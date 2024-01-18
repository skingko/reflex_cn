---

components:
    - rx.chakra.Popover
    - rx.chakra.PopoverTrigger
    - rx.chakra.PopoverContent
    - rx.chakra.PopoverHeader
    - rx.chakra.PopoverBody
    - rx.chakra.PopoverFooter
    - rx.chakra.PopoverArrow
    - rx.chakra.PopoverAnchor
---

```python exec
import reflex as rx
```

# 弹出框

弹出框是一个浮动在触发器周围的非模态对话框。
它用于向用户显示上下文信息，并应与可点击的触发元素配对使用。

```python demo
rx.popover(
    rx.popover_trigger(rx.button("Popover Example")),
    rx.popover_content(
        rx.popover_header("Confirm"),
        rx.popover_body("Do you want to confirm example?"),
        rx.popover_footer(rx.text("Footer text.")),
        rx.popover_close_button(),
    ),
)
```

