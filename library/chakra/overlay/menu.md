---

components:
    - rx.chakra.Menu
    - rx.chakra.MenuButton
    - rx.chakra.MenuList
    - rx.chakra.MenuItem
    - rx.chakra.MenuDivider
    - rx.chakra.MenuGroup
    - rx.chakra.MenuOptionGroup
    - rx.chakra.MenuItemOption
---

```python exec
import reflex as rx
```

# 菜单

一种常见的下拉菜单按钮设计模式的可访问下拉菜单。

```python demo
rx.menu(
    rx.menu_button("Menu"),
    rx.menu_list(
        rx.menu_item("Example"),
        rx.menu_divider(),
        rx.menu_item("Example"),
        rx.menu_item("Example"),
    ),
)
```

