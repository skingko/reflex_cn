```python exec
import reflex as rx

from pcweb.pages.docs import vars
```

# 渲染可迭代对象

您经常希望从数据集合中显示多个相似的组件。`rx.foreach` 组件接受一个可迭代对象（列表、元组或字典）和一个渲染列表中每个项目的函数。这对于动态渲染在状态中定义的项目列表非常有用。

在这个简单的示例中，我们遍历一个颜色列表，并渲染每个颜色的名称，并将其作为 `rx.box` 的背景颜色使用。正如我们所看到的，我们有一个函数 `colored_box`，我们将其传递给 `rx.foreach` 组件。此函数渲染我们作为状态变量 `color` 定义的列表中的每个项目。

```python demo exec
class IterState(rx.State):
    color: list[str] = [
        "red",
        "green",
        "blue",
        "yellow",
        "orange",
        "purple",
    ]


def colored_box(color: str):
    return rx.box(rx.text(color), background_color=color)


def simple_foreach():
    return rx.responsive_grid(
        rx.foreach(IterState.color, colored_box),
        columns=[2, 4, 6],
    )

```

```md alert warning
# The type signature of the functions does not matter to the `foreach` component. It's the type annotation on the `state var` that determines what operations are available (e.g. when nesting).
```

## 枚举

该函数还可以将索引作为第二个参数传入，这意味着我们可以按照所示的示例对数据进行枚举。

```python demo exec
class IterIndexState(rx.State):
    color: list[str] = [
        "red",
        "green",
        "blue",
        "yellow",
        "orange",
        "purple",
    ]


def enumerate_foreach():
    return rx.responsive_grid(
        rx.foreach(
            IterIndexState.color,
            lambda color, index: rx.box(rx.text(index), bg=color)
        ),
        columns=[2, 4, 6],
    )

```

## 字典

我们可以使用 `foreach` 遍历字典数据结构。当将字典传递给渲染每个项目的函数时，它呈现为键值对列表 `[("sky", "blue"), ("balloon", "red"), ("grass", "green")]`。

```python demo exec
class SimpleDictIterState(rx.State):
    color_chart: dict[str, str] = {
        "sky": "blue",
        "balloon": "red",
        "grass": "green",
    }


def display_color(color: list):
    # color is presented as a list key-value pairs [("sky", "blue"), ("balloon", "red"), ("grass", "green")]
    return rx.box(rx.text(color[0]), bg=color[1], padding_x="1.5em")


def dict_foreach():
    return rx.responsive_grid(
        rx.foreach(
            SimpleDictIterState.color_chart,
            display_color,
        ),
        columns=[2, 4, 6],
    )

```

## 嵌套示例

`rx.foreach` 可用于嵌套状态变量。在这里，我们使用嵌套的 `foreach` 组件来渲染嵌套的状态变量。`project_item` 函数内部的 `rx.foreach(project["technologies"], get_badge)` 将渲染类型为 `list` 的 `dict` 值。`projects_example` 函数内部的 `rx.box(rx.foreach(NestedStateFE.projects, project_item))` 将渲染整个状态变量 `projects` 中的每个 `dict`。

```python demo exec
class NestedStateFE(rx.State):
    projects: list[dict[str, list]] = [
        {
            "technologies": ["Next.js", "Prisma", "Tailwind", "Google Cloud", "Docker", "MySQL"]
        },
        {
            "technologies": ["Python", "Flask", "Google Cloud", "Docker"]
        }
    ]

def get_badge(technology: str) -> rx.Component:
    return rx.badge(technology, variant="subtle", color_scheme="green")

def project_item(project: dict) -> rx.Component:
    return rx.box(
        rx.hstack(            
            rx.foreach(project["technologies"], get_badge)
        ),
    )

def projects_example() -> rx.Component:
    return rx.box(rx.foreach(NestedStateFE.projects, project_item))
```

如果您想要一个示例，其中字典中的值并非都是相同类型，请查看[使用 foreach 进行变量操作]({vars.var_operations.path}) 上的示例。

下面是一个使用嵌套数据结构和 `foreach` 的进一步示例。

```python demo exec
class NestedDictIterState(rx.State):
    color_chart: dict[str, list[str]] = {
        "purple": ["red", "blue"],
        "orange": ["yellow", "red"],
        "green": ["blue", "yellow"],
    }


def display_colors(color: list[str, list[str]]):
    
    return rx.vstack(
        rx.text(color[0], color=color[0]),
        rx.hstack(
            rx.foreach(
                color[1],
                lambda x: rx.box(
                    rx.text(x, color="black"), bg=x
                ),
            )
        ),
    )


def nested_dict_foreach():
    return rx.responsive_grid(
        rx.foreach(
            NestedDictIterState.color_chart,
            display_colors,
        ),
        columns=[2, 4, 6],
    )

```

## 使用 Cond 进行 Foreach

我们还可以使用 `foreach` 结合 `cond` 组件。

在这个示例中，我们定义了函数 `render_item`。该函数接受一个 `item`，使用 `cond` 来检查 `is_packed` 是否为真。如果已打包，则返回带有 `✔` 的 `item_name`，否则仅返回 `item_name`。我们使用 `foreach` 来使用 `render_item` 函数迭代遍历 `to_do_list` 中的所有项目。

```python demo exec
class ToDoListItem(rx.Base):
    item_name: str
    is_packed: bool

class ForeachCondState(rx.State):
    to_do_list: list[ToDoListItem] = [
        ToDoListItem(item_name="Space suit", is_packed=True), 
        ToDoListItem(item_name="Helmet", is_packed=True),
        ToDoListItem(item_name="Back Pack", is_packed=False),
        ]


def render_item(item: [str, bool]):
    return rx.cond(
        item.is_packed, 
        rx.list_item(item.item_name + ' ✔'),
        rx.list_item(item.item_name),
        )

def packing_list():
    return rx.vstack(
        rx.text("Sammy's Packing List", as_="strong"),
        rx.list(rx.foreach(ForeachCondState.to_do_list, render_item)),
    )

```

