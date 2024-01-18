---

components:
    - rx.chakra.Modal
    - rx.chakra.ModalOverlay
    - rx.chakra.ModalContent
    - rx.chakra.ModalHeader
    - rx.chakra.ModalBody
    - rx.chakra.ModalFooter
---

```python exec
import reflex as rx
```

# 模态框

模态框是以覆盖在主窗口或其他对话框窗口上的窗口。模态框背后的内容是不活动的，意味着用户无法与其进行交互。

```python demo exec
class ModalState(rx.State):
    show: bool = False

    def change(self):
        self.show = not (self.show)


def modal_example():
    return rx.vstack(
    rx.button("Confirm", on_click=ModalState.change),
    rx.modal(
        rx.modal_overlay(
            rx.modal_content(
                rx.modal_header("Confirm"),
                rx.modal_body("Do you want to confirm example?"),
                rx.modal_footer(rx.button("Close", on_click=ModalState.change)),
            )
        ),
        is_open=ModalState.show,
    ),
)
```

