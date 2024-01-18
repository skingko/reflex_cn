---
components:
    - rx.radix.themes.ContextMenuRoot  <!--\[to_be_replace0\]-->
    - rx.radix.themes.ContextMenuItem  <!--\[to_be_replace1\]-->
    - rx.radix.themes.ContextMenuSeparator  <!--\[to_be_replace2\]-->
    - rx.radix.themes.ContextMenuTrigger  <!--\[to_be_replace3\]-->
    - rx.radix.themes.ContextMenuContent  <!--\[to_be_replace4\]-->
    - rx.radix.themes.ContextMenuSub  <!--\[to_be_replace5\]-->
    - rx.radix.themes.ContextMenuSubTrigger  <!--\[to_be_replace6\]-->
    - rx.radix.themes.ContextMenuSubContent  <!--\[to_be_replace7\]-->
---


```python exec
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
```

# 上下文菜单

上下文菜单是在用户交互（比如右键点击或悬停）时出现的弹出菜单。

## 基本使用

上下文菜单由 `ContextMenuTrigger`（触发器）和 `ContextMenuContent`（菜单内容）组成。`ContextMenuTrigger`是用户与之交互以打开菜单的元素。`ContextMenuContent`则是菜单本身。

```python demo
contextmenu_root(
    contextmenu_trigger(
       button("Right click me"),
    ),
    contextmenu_content(
        contextmenu_item("Edit", shortcut="⌘ E"),
        contextmenu_item("Duplicate", shortcut="⌘ D"),
        contextmenu_separator(),
        contextmenu_item("Archive", shortcut="⌘ N"),
        contextmenu_sub(
            contextmenu_sub_trigger("More"),
            contextmenu_sub_content(
                contextmenu_item("Move to project…"),
                contextmenu_item("Move to folder…"),
                contextmenu_separator(),
                contextmenu_item("Advanced options…"),
            ),
        ),
        contextmenu_separator(),
        contextmenu_item("Share"),
        contextmenu_item("Add to favorites"),
        contextmenu_separator(),
        contextmenu_item("Delete", shortcut="⌘ ⌫", color="red"),
    ),
)
```


```python demo
grid(
    contextmenu_root(
        contextmenu_trigger(
            button("Right click me"),
        ),
        contextmenu_content(
            contextmenu_item("Edit", shortcut="⌘ E"),
            contextmenu_item("Duplicate", shortcut="⌘ D"),
            contextmenu_separator(),
            contextmenu_item("Archive", shortcut="⌘ N"),
            contextmenu_separator(),
            contextmenu_item("Delete", shortcut="⌘ ⌫", color="red",
            ),
            size="1",
        ),
    ),
    contextmenu_root(
        contextmenu_trigger(
             button("Right click me"),
        ),
        contextmenu_content(
            contextmenu_item("Edit", shortcut="⌘ E"),
            contextmenu_item("Duplicate", shortcut="⌘ D"),
            contextmenu_separator(),
            contextmenu_item("Archive", shortcut="⌘ N"),
            contextmenu_separator(),
            contextmenu_item("Delete", shortcut="⌘ ⌫", color="red"
            ),
            size="2",
        ),
    ),
    columns="2", 
    gap="3",
)
```

