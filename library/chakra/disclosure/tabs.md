---
components:
    - rx.chakra.Tabs
    - rx.chakra.TabList
    - rx.chakra.Tab
    - rx.chakra.TabPanel
    - rx.chakra.TabPanels
---

```python exec
import reflex as rx
```

# 标签页

标签页组件允许您在容器内的多个页面中显示内容。这些页面由标签列表组织，相应的标签面板可以接受子组件。

```python demo
rx.tabs(
    rx.tab_list(
        rx.tab("Tab 1"),
        rx.tab("Tab 2"),
        rx.tab("Tab 3"),
    ),
    rx.tab_panels(
        rx.tab_panel(rx.text("Text from tab 1.")),
        rx.tab_panel(rx.checkbox("Text from tab 2.")),
        rx.tab_panel(rx.button("Text from tab 3.", color="black")),
    ),
    bg="black",
    color="white",
    shadow="lg",
)
```

您可以使用简写语法创建标签页组件。将一个元组列表传递给`items`属性。每个元组应包含一个标签和一个面板。

```python demo
rx.tabs(
    items = [("Tab 1", rx.text("Text from tab 1.")), ("Tab 2", rx.checkbox("Text from tab 2.")), ("Tab 3", rx.button("Text from tab 3.", color="black"))],
    bg="black",
    color="white",
    shadow="lg",
)
```

