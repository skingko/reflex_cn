```python exec
import random
import time

import reflex as rx

from pcweb.pages.docs import vars
```
# 基础变量

变量是应用程序中可能随时间变化的任何字段。变量直接呈现在应用程序前端。

基础变量被定义为状态类中的字段。

它们可以有预设的默认值。如果不提供默认值，则必须提供类型注释。

```md alert warning
# State Vars should provide type annotations.
Reflex relies on type annotations to determine the type of state vars during the compilation process.
```

```python demo exec
class TickerState(rx.State):
    ticker: str ="AAPL"
    price: str = "$150"


def ticker_example():
    return rx.stat_group(
        rx.stat(
            rx.stat_label(TickerState.ticker),
            rx.stat_number(TickerState.price),
            rx.stat_help_text(
                rx.stat_arrow(type_="increase"),
                "4%",
            ),
        ),
    )
```

在此示例中，`ticker`和`price`是应用程序中的基础变量，在运行时可以进行修改。

```md alert warning
# Vars must be JSON serializable.
Vars are used to communicate between the frontend and backend. They must be primitive Python types, Plotly figures, Pandas dataframes, or [a custom defined type]({vars.custom_vars.path}).
```

## 仅后端变量

在状态类中以下划线开头的任何变量都被视为仅后端变量，不会与前端同步。与前端无关的与特定会话关联的数据应存储在仅后端变量中，以减少网络流量并提高性能。

它们的优点在于它们不需要进行JSON序列化，但仍需可通过cloudpickle在生产模式下与Redis一起使用。它们无法直接在前端渲染，并且可用于存储不应发送给客户端的敏感值。

例如，仅后端变量可用于存储大型数据结构，然后使用缓存变量将数据分页到前端。

```python demo exec
import numpy as np


class BackendVarState(rx.State):
    _backend: np.ndarray = np.array([random.randint(0, 100) for _ in range(100)])
    offset: int = 0
    limit: int = 10

    @rx.cached_var
    def page(self) -> list[int]:
        return [
            int(x)  # explicit cast to int
            for x in self._backend[self.offset : self.offset + self.limit]
        ]

    @rx.cached_var
    def page_number(self) -> int:
        return (self.offset // self.limit) + 1 + (1 if self.offset % self.limit else 0)

    @rx.cached_var
    def total_pages(self) -> int:
        return len(self._backend) // self.limit + (1 if len(self._backend) % self.limit else 0)

    def prev_page(self):
        self.offset = max(self.offset - self.limit, 0)

    def next_page(self):
        if self.offset + self.limit < len(self._backend):
            self.offset += self.limit

    def generate_more(self):
        self._backend = np.append(self._backend, [random.randint(0, 100) for _ in range(random.randint(0, 100))])


def backend_var_example():
    return rx.vstack(
        rx.hstack(
            rx.button(
                "Prev",
                on_click=BackendVarState.prev_page,
            ),
            rx.text(f"Page {BackendVarState.page_number} / {BackendVarState.total_pages}"),
            rx.button(
                "Next",
                on_click=BackendVarState.next_page,
            ),
            rx.text("Page Size"),
            rx.number_input(
                width="5em",
                value=BackendVarState.limit,
                on_change=BackendVarState.set_limit,
            ),
            rx.button("Generate More", on_click=BackendVarState.generate_more),
        ),
        rx.list(
            rx.foreach(
                BackendVarState.page,
                lambda x, ix: rx.text(f"_backend[{ix + BackendVarState.offset}] = {x}"),
            ),
        ),
    )
```

