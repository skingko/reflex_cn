翻译成中文：

---
components:
    - rx.chakra.Drawer
    - rx.chakra.DrawerOverlay
    - rx.chakra.DrawerContent
    - rx.chakra.DrawerHeader
    - rx.chakra.DrawerBody
    - rx.chakra.DrawerFooter
---

```python exec
import reflex as rx
```

# 抽屉

抽屉组件是从屏幕边缘滑出的面板。
当您需要用户完成任务或查看一些详细信息而不离开当前页面时，它非常有用。

```python demo exec
class DrawerState(rx.State):
    show_right: bool = False
    show_top: bool = False

    def top(self):
        self.show_top = not (self.show_top)

    def right(self):
        self.show_right = not (self.show_right)

def drawer_example():
    return rx.vstack(
        rx.button("Show Right Drawer", on_click=DrawerState.right),
        rx.drawer(
            rx.drawer_overlay(
                rx.drawer_content(
                    rx.drawer_header("Confirm"),
                    rx.drawer_body("Do you want to confirm example?"),
                    rx.drawer_footer(
                        rx.button("Close", on_click=DrawerState.right)
                    ),
                    bg = "rgba(0, 0, 0, 0.3)"
                )
            ),
            is_open=DrawerState.show_right,
        )
    )
```

抽屉可以从顶部、底部、左侧或右侧显示。
默认情况下，如上所示，它显示在右侧。

```python demo
rx.vstack(
    rx.button("Show Top Drawer", on_click=DrawerState.top),
    rx.drawer(
        rx.drawer_overlay(
            rx.drawer_content(
                rx.drawer_header("Confirm"),
                rx.drawer_body("Do you want to confirm example?"),
                rx.drawer_footer(
                    rx.button("Close", on_click=DrawerState.top)
                ),
            )
        ),
        placement="top",
        is_open=DrawerState.show_top,
    )
)
```

