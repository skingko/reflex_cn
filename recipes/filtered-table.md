```python exec
import reflex as rx
```

# 过滤表格

## 配方

```python eval
rx.center(rx.image(src="/gallery/filtered_table.gif"))
```

该配方使用`rx.foreach`来生成行，并使用计算变量对数据进行过滤，使用一个输入值作为过滤值。

此外，过滤输入使用了防抖动的方式限制更新，这样可以防止在每次按键时计算过滤数据。

```python
import reflex as rx
from typing import List, Dict

RAW_DATA = [
    \{"name": "Alice", "tags": "tag1"},
    \{"name": "Bob", "tags": "tag2"},
    \{"name": "Charlie", "tags": "tag1"},
]
RAW_DATA_COLUMNS = ["Name", "tags"]


class FilteredTableState(rx.State):
    filter_expr: str = ""
    data: Dict[str, Dict[str, str]] = RAW_DATA

    @rx.cached_var
    def filtered_data(self) -> List[Dict[str, str]]:
        # Use this generated filtered data view in the `rx.foreach` of
        #  the table renderer of rows
        # It is dependent on `filter_expr`
        # This `filter_expr` is set by an rx.input
        return [
            row
            for row in self.data
            if self.filter_expr == ""
            or self.filter_expr != ""
            and self.filter_expr == row["tags"]
        ]

    def input_filter_on_change(self, value):
        self.filter_expr = value
        # for DEBUGGING
        yield rx.console_log(f"Filter set to: \{self.filter_expr}")


def render_row(row):
    return rx.tr(rx.td(row["name"]), rx.td(row["tags"]))


def render_rows():
    return [
        rx.foreach(
            # use data filtered by `filter_expr` as update by rx.input
            FilteredTableState.filtered_data,
            render_row,
        )
    ]


def render_table():
    return rx.table_container(
        rx.table(
            rx.thead(rx.tr(*[rx.th(column) for column in RAW_DATA_COLUMNS])),
            rx.tbody(*render_rows()),
        )
    )


def index() -> rx.Component:
    return rx.box(
        rx.box(
            rx.heading(
                "Filter by tags:",
                size="sm",
            ),
            rx.input(
                on_change=FilteredTableState.input_filter_on_change,
                value=FilteredTableState.filter_expr,
                debounce_timeout=1000,
            ),
        ),
        rx.box(
            render_table(),
        ),
    )


app = rx.App()
app.add_page(index, route="/")
```

