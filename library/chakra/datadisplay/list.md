---

components:
    - rx.chakra.List（列表）
    - rx.chakra.ListItem（列表项）
    - rx.chakra.UnorderedList（无序列表）
    - rx.chakra.OrderedList（有序列表）

---

```python exec
import reflex as rx
```

# 列表

有三种类型的列表：普通列表、有序列表和无序列表。

创建列表的速记语法是通过传入一个项目列表。
这些项目可以是组件或Python原始值。

```python demo
rx.list(
    items=["Example 1", "Example 2", "Example 3"],
    spacing=".25em"
)
```

下面的示例使用了显式的列表语法和列表项语法。
普通列表用于显示一系列项目。
它们没有项目符号或编号，并且将列表项垂直堆叠。

```python demo
rx.list(
    rx.list_item("Example 1"),
    rx.list_item("Example 2"),
    rx.list_item("Example 3"),
)
```

无序列表具有项目符号来显示列表项。

```python demo
rx.unordered_list(
    rx.list_item("Example 1"),
    rx.list_item("Example 2"),
    rx.list_item("Example 3"),
)
```

有序列表具有编号来显示列表项。

```python demo
rx.ordered_list(
    rx.list_item("Example 1"),
    rx.list_item("Example 2"),
    rx.list_item("Example 3"),
)
```

列表还可以与图标一起使用。

```python demo
rx.list(
    rx.list_item(rx.icon(tag="check_circle", color = "green"), "Allowed"),
    rx.list_item(rx.icon(tag="not_allowed", color = "red"), "Not"),
    rx.list_item(rx.icon(tag="settings", color = "grey"), "Settings"),
    spacing = ".25em"
)
```

