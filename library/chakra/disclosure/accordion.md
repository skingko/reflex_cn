---

组件：
  - rx.chakra.Accordion
  - rx.chakra.AccordionItem
  - rx.chakra.AccordionButton
  - rx.chakra.AccordionPanel
  - rx.chakra.AccordionIcon

```python exec
import reflex as rx
```

# 折叠面板

折叠面板允许您在标题下隐藏和显示容器中的内容。

折叠面板由外部折叠面板组件和内部折叠面板项组成。
每个项都有一个可选的按钮和面板。按钮用于切换面板的可见性。

```python demo
rx.accordion(
    rx.accordion_item(
        rx.accordion_button(
            rx.heading("Example"),
            rx.accordion_icon(),
        ),
        rx.accordion_panel(
            rx.text("This is an example of an accordion component.")
        )
    ),
    allow_toggle = True,
    width = "100%"
)
```

折叠面板可以有多个项目。

```python demo
rx.accordion(
    rx.accordion_item(
        rx.accordion_button(
            rx.heading("Example 1"),
            rx.accordion_icon(),
        ),
        rx.accordion_panel(
            rx.text("This is an example of an accordion component.")
        ),
    ),
    rx.accordion_item(
        rx.accordion_button(
            rx.heading("Example 2"),
            rx.accordion_icon(),
        ),
        rx.accordion_panel(
            rx.text("This is an example of an accordion component.")
        ),
    ),
    allow_multiple = True,
    bg="black",
    color="white",
    width = "100%"
)
```

通过将折叠面板嵌套在外部折叠面板内部，您还可以创建多级折叠面板。

```python demo
rx.accordion(
    rx.accordion_item(
        rx.accordion_button(
            rx.accordion_icon(),
            rx.heading("Outer"),
            
        ),
        rx.accordion_panel(
            rx.accordion(
            rx.accordion_item(
                rx.accordion_button(
                    rx.accordion_icon(),
                    rx.heading("Inner"),    
                ),
                rx.accordion_panel(
                    rx.badge("Inner Panel", variant="solid", color_scheme="green"),
                )
            )
            ),
        )  
    ),
    width = "100%"
)
```

您还可以使用简写语法创建折叠面板。
将一个元组的列表传递给`items`属性。
每个元组应包含一个标签和一个面板。

```python demo
rx.accordion(
   items=[("Label 1", rx.center("Panel 1")), ("Label 2", rx.center("Panel 2"))],
   width="100%"
)
```

