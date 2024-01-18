```yaml
components:
    - rx.chakra.Table
    - rx.chakra.TableCaption
    - rx.chakra.Thead
    - rx.chakra.Tbody
    - rx.chakra.Tfoot
    - rx.chakra.Tr
    - rx.chakra.Th
    - rx.chakra.Td
    - rx.chakra.TableContainer
```

```python exec
import reflex as rx
```

# 表格

表格用于有效组织和展示数据。
表格组件与 `data_table` 组件不同之处在于它不适用于展示大量数据。
它适用于以更有组织的方式展示数据。

可以使用简写语法或显式创建表格组件来创建表格。
简写语法适用于简单的表格，但如果您需要对表格进行更多控制，可以使用显式语法。

让我们从简写语法开始。
简写语法有 `headers`、`rows` 和 `footers` 属性。

```python demo
rx.table_container(
    rx.table(
        headers=["Name", "Age", "Location"],
        rows=[
            ("John", 30, "New York"),
            ("Jane", 31, "San Francisco"),
            ("Joe", 32, "Los Angeles")
        ],
        footers=["Footer 1", "Footer 2", "Footer 3"],
        variant='striped'
    )
)
```

让我们显式地创建一个简单的表格。在这个示例中，我们将创建一个有两列的表格：`姓名` 和 `年龄`。

```python demo
rx.table(
    rx.thead(
        rx.tr(
            rx.th("Name"),
            rx.th("Age"),
        )
    ),
    rx.tbody(
        rx.tr(
            rx.td("John"),
            rx.td(30),
        )
    ),
)
```

在示例中，我们将使用这些数据在表格中展示。

```python exec
columns = ["Name", "Age", "Location"]
data = [
    ["John", 30, "New York"],
    ["Jane", 25, "San Francisco"],
]
footer = ["Footer 1", "Footer 2", "Footer 3"]
```

```python
columns = ["Name", "Age", "Location"]
data = [
    ["John", 30, "New York"],
    ["Jane", 25, "San Francisco"],
]
footer = ["Footer 1", "Footer 2", "Footer 3"]
```

现在让我们使用创建的数据创建一个表格。

```python eval
rx.center(
    rx.table_container(
        rx.table(
            rx.table_caption("Example Table"),
            rx.thead(
                rx.tr(
                    *[rx.th(column) for column in columns]
                )
            ),
            rx.tbody(
                *[rx.tr(*[rx.td(item) for item in row]) for row in data]
            ),
            rx.tfoot(
                rx.tr(
                    *[rx.th(item) for item in footer]
                )
            ),
        )
    )
)
```

表格还可以通过 variant 和 color_scheme 参数进行样式设置。

```python demo
rx.table_container(
    rx.table(
        rx.thead(
        rx.tr(
            rx.th("Name"),
            rx.th("Age"),
            rx.th("Location"),
            )
        ),
        rx.tbody(
            rx.tr(
                rx.td("John"),
                rx.td(30),
                rx.td("New York"),
            ),
            rx.tr(
                rx.td("Jane"), 
                rx.td(31),
                rx.td("San Francisco"),
            ),
            rx.tr(
                rx.td("Joe"),
                rx.td(32),
                rx.td("Los Angeles"),
            )
        ),
        variant='striped',
        color_scheme='teal'
    )
)
```

