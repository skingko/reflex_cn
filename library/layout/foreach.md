---

components:
    - rx.Foreach
---

```python exec
import reflex as rx
```

# Foreach

`rx.foreach`组件接受一个可迭代对象（列表、元组或字典）和一个渲染列表中每个项目的函数。
这对于动态渲染在状态中定义的项目列表非常有用。

```python demo exec
from typing import List
class ForeachState(rx.State):
    color: List[str] = ["red", "green", "blue", "yellow", "orange", "purple"]

def colored_box(color: str):
    return rx.box(
        rx.text(color),
        bg=color
    )

def foreach_example():
    return rx.responsive_grid(
        rx.foreach(
            ForeachState.color,
            colored_box
        ),
        columns=[2, 4, 6],
    )
```

该函数还可以接受一个索引作为第二个参数。

```python demo exec
def colored_box_index(color: str, index: int):
    return rx.box(
        rx.text(index),
        bg=color
    )

def foreach_example_index():
    return rx.responsive_grid(
        rx.foreach(
            ForeachState.color,
            lambda color, index: colored_box_index(color, index)
        ),
        columns=[2, 4, 6],
    )
```

可以使用嵌套的foreach组件来渲染嵌套列表。

当索引到嵌套列表时，将列表的类型声明为Reflex需要进行类型检查是很重要的。
这确保在用户遇到之前捕获任何潜在的前端JS错误。

```python demo exec
from typing import List

class NestedForeachState(rx.State):
    numbers: List[List[str]] = [["1", "2", "3"], ["4", "5", "6"], ["7", "8", "9"]]

def display_row(row):
    return rx.hstack(
        rx.foreach(
            row,
            lambda item: rx.box(
                item,
                border="1px solid black",
                padding="0.5em",
            )
        ),
    )

def nested_foreach_example():
    return rx.vstack(
        rx.foreach(
             NestedForeachState.numbers,
            display_row
        )
    )
```

下面是一个更复杂的foreach在待办事项列表中的示例。

```python demo exec
from typing import List
class ListState(rx.State):
    items: List[str] = ["Write Code", "Sleep", "Have Fun"]
    new_item: str

    def add_item(self):
        self.items += [self.new_item]

    def finish_item(self, item: str):
        self.items = [i for i in self.items if i != item]

def get_item(item):
    return rx.list_item(
        rx.hstack(
            rx.button(
                on_click=lambda: ListState.finish_item(item),
                height="1.5em",
                background_color="white",
                border="1px solid blue",
            ),
            rx.text(item, font_size="1.25em"),
        ),
    )

def todo_example():
    return rx.vstack(
        rx.heading("Todos"),
        rx.input(on_blur=ListState.set_new_item, placeholder="Add a todo...", bg  = "white"),
        rx.button("Add", on_click=ListState.add_item, bg = "white"),
        rx.divider(),
        rx.ordered_list(
            rx.foreach(
                ListState.items,
                get_item,
            ),
        ),
        bg = "#ededed",
        padding = "1em",
        border_radius = "0.5em",
        shadow = "lg"
    )
```

## 字典

可以将字典中的项目作为键值对列表访问。
使用颜色示例，我们可以稍微修改代码以使用字典，如下所示。

```python demo exec
from typing import List
class SimpleDictForeachState(rx.State):
    color_chart: dict[int, str] = {
         1 : "blue",
         2: "red",
         3: "green"
    }

def display_color(color: List):
    # color is presented as a list key-value pair([1, "blue"],[2, "red"], [3, "green"])
    return rx.box(rx.text(color[0]), bg=color[1])


def foreach_dict_example():
    return rx.responsive_grid(
        rx.foreach(
            SimpleDictForeachState.color_chart,
            display_color
        ),
        columns = [2, 4, 6]
    )
```

现在我们来展示一个更复杂的字典示例，使用颜色示例。
假设我们想显示一个包含次要颜色作为键和它们所包含的主要颜色作为值的字典，我们可以修改代码如下：

```python demo exec
from typing import List, Dict
class ComplexDictForeachState(rx.State):
    color_chart: Dict[str, List[str]] = {
        "purple": ["red", "blue"],
        "orange": ["yellow", "red"],
        "green": ["blue", "yellow"]
    }

def display_colors(color: List):
    return rx.vstack(
            rx.text(color[0], color=color[0]),
            rx.hstack(
                rx.foreach(
                    color[1], lambda x: rx.box(rx.text(x, color="black"), bg=x)
                )

            )
        )

def foreach_complex_dict_example():
    return rx.responsive_grid(
        rx.foreach(
            ComplexDictForeachState.color_chart,
            display_colors
        ),
        columns=[2, 4, 6]
    )
```

