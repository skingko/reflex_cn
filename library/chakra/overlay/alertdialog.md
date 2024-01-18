---

components:
    - rx.chakra.AlertDialog
    - rx.chakra.AlertDialogOverlay
    - rx.chakra.AlertDialogContent
    - rx.chakra.AlertDialogHeader
    - rx.chakra.AlertDialogBody
    - rx.chakra.AlertDialogFooter
---

```python exec
import reflex as rx
```

# 弹窗对话框

弹窗对话框组件用于中断用户并进行必要的确认或处理事件。
该组件会在页面上方弹出，提示用户完成某个事件。

```python demo exec
class AlertDialogState(rx.State):
    show: bool = False

    def change(self):
        self.show = not (self.show)


def alertdialog_example():
    return rx.vstack(
        rx.button("Show Alert Dialog", on_click=AlertDialogState.change),
        rx.alert_dialog(
            rx.alert_dialog_overlay(
                rx.alert_dialog_content(
                    rx.alert_dialog_header("Confirm"),
                    rx.alert_dialog_body("Do you want to confirm example?"),
                    rx.alert_dialog_footer(
                        rx.button("Close", on_click=AlertDialogState.change)
                    ),
                )
            ),
            is_open=AlertDialogState.show,
        ),
        width="100%",
    )
```

