---
components:
    - rx.radix.themes.DropdownMenuRoot
    - rx.radix.themes.DropdownMenuContent
    - rx.radix.themes.DropdownMenuTrigger
    - rx.radix.themes.DropdownMenuItem
    - rx.radix.themes.DropdownMenuSeparator
    - rx.radix.themes.DropdownMenuSubContent
---

```python exec
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
```


# 下拉菜单

下拉菜单是一个菜单，它提供了用户可以从中选择的选项列表。它们通常位于一个控制它们出现和消失的按钮附近。

```python demo
dropdownmenu_root(
    dropdownmenu_trigger(
        button("Options", variant="soft"),
    ),
    dropdownmenu_content(
        dropdownmenu_item("Edit", shortcut="⌘ E"),
        dropdownmenu_item("Duplicate", shortcut="⌘ D"),
        dropdownmenu_separator(),
        dropdownmenu_item("Archive", shortcut="⌘ N"),
        dropdownmenu_sub(
            dropdownmenu_sub_trigger("More"),
            dropdownmenu_sub_content(
                dropdownmenu_item("Move to project…"),
                dropdownmenu_item("Move to folder…"),
                dropdownmenu_separator(),
                dropdownmenu_item("Advanced options…"),
            ),
        ),
        dropdownmenu_separator(),
        dropdownmenu_item("Share"),
        dropdownmenu_item("Add to favorites"),
        dropdownmenu_separator(),
        dropdownmenu_item("Delete", shortcut="⌘ ⌫", color="red"),
    ),
)
```

# 大小

```python demo
flex(
    dropdownmenu_root(
        dropdownmenu_trigger(
            button("Options", variant="soft", size="2"),
        ),
        dropdownmenu_content(
            dropdownmenu_item("Edit", shortcut="⌘ E"),
            dropdownmenu_item("Duplicate", shortcut="⌘ D"),
            dropdownmenu_separator(),
            dropdownmenu_item("Archive", shortcut="⌘ N"),
            dropdownmenu_separator(),
            dropdownmenu_item("Delete", shortcut="⌘ ⌫", color="red"),
            size="2",
        ),
    ),
    dropdownmenu_root(
        dropdownmenu_trigger(
            button("Options", variant="soft", size="1"),
        ),
        dropdownmenu_content(
            dropdownmenu_item("Edit", shortcut="⌘ E"),
            dropdownmenu_item("Duplicate", shortcut="⌘ D"),
            dropdownmenu_separator(),
            dropdownmenu_item("Archive", shortcut="⌘ N"),
            dropdownmenu_separator(),
            dropdownmenu_item("Delete", shortcut="⌘ ⌫", color="red"),
            size="1",
        ),
    ),
    gap="3", 
    align="center",
)
```

