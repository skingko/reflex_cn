---
components:
    - rx.recharts.PieChart
---

```python exec
import reflex as rx
from pcweb.templates.docpage import docgraphing

data01 = [
  {
    "name": "Group A",
    "value": 400
  },
  {
    "name": "Group B",
    "value": 300
  },
  {
    "name": "Group C",
    "value": 300
  },
  {
    "name": "Group D",
    "value": 200
  },
  {
    "name": "Group E",
    "value": 278
  },
  {
    "name": "Group F",
    "value": 189
  }
]
data02 = [
  {
    "name": "Group A",
    "value": 2400
  },
  {
    "name": "Group B",
    "value": 4567
  },
  {
    "name": "Group C",
    "value": 1398
  },
  {
    "name": "Group D",
    "value": 9800
  },
  {
    "name": "Group E",
    "value": 3908
  },
  {
    "name": "Group F",
    "value": 4800
  }
]

pie_chart_simple_example = """rx.recharts.pie_chart(
                rx.recharts.pie(
                    data=data01,
                    data_key="value",
                    name_key="name",
                    cx="50%",
                    cy="50%",
                    fill="#8884d8",
                    label=True,
                    )
                    )"""

pie_chart_complex_example = """rx.recharts.pie_chart(
                  rx.recharts.pie(
                    data=data01,
                    data_key="value",
                    name_key="name",
                    cx="50%",
                    cy="50%",
                    fill="#82ca9d",
                    inner_radius="60%",
                    ),
                    rx.recharts.pie(
                    data=data02,
                    data_key="value",
                    name_key="name",
                    cx="50%",
                    cy="50%",
                    fill="#8884d8",
                    outer_radius="50%",
                    ),
                    rx.recharts.graphing_tooltip(),
                    )"""

```

一个饼图是一种将数据按比例划分为扇形，用于展示统计信息的图形。

对于一个饼图，我们需要为我们想要绘制的每组数值定义一个 `rx.recharts.pie()` 组件。每个 `rx.recharts.pie()` 组件都具有一个 `data`，一个 `data_key` 和一个 `name_key` ，清楚地指定了我们要跟踪的数据和数据中的哪些变量。在这个简单的例子中，我们将 `value` 列作为我们的 `data_key` 绘制，将 `name` 列设置为我们的 `name_key`。

```python eval
docgraphing(pie_chart_simple_example, comp=eval(pie_chart_simple_example),  data =  "data01=" + str(data01))
```

我们还可以使用两个 `rx.recharts.pie` 组件在一个图表上添加两个饼图。

```python eval
docgraphing(pie_chart_complex_example, comp=eval(pie_chart_complex_example),  data =  "data01=" + str(data01) + "&data02=" + str(data02))
```

# 动态数据

将图表数据与状态变量关联，在状态变化时自动更新图表，为对用户界面元素的响应可视化数据提供了一种很好的方式。查看 "Data" 标签以查看驱动这个半饼图的子状态。

```python exec
from typing import Any


class PieChartState(rx.State):
    resources: list[dict[str, Any]] = [
        dict(type_="🏆", count=1),
        dict(type_="🪵", count=1),
        dict(type_="🥑", count=1),
        dict(type_="🧱", count=1),
    ]

    @rx.cached_var
    def resource_types(self) -> list[str]:
        return [r["type_"] for r in self.resources]

    def increment(self, type_: str):
        for resource in self.resources:
            if resource["type_"] == type_:
                resource["count"] += 1
                break

    def decrement(self, type_: str):
        for resource in self.resources:
            if resource["type_"] == type_ and resource["count"] > 0:
                resource["count"] -= 1
                break


pie_chart_state_example = """
rx.hstack(
    rx.recharts.pie_chart(
        rx.recharts.pie(
            data=PieChartState.resources,
            data_key="count",
            name_key="type_",
            cx="50%",
            cy="50%",
            start_angle=180,
            end_angle=0,
            fill="#8884d8",
            label=True,
        ),
        rx.recharts.graphing_tooltip(),
    ),
    rx.vstack(
        rx.foreach(
            PieChartState.resource_types,
            lambda type_, i: rx.hstack(
                rx.button("-", on_click=PieChartState.decrement(type_)),
                rx.text(type_, PieChartState.resources[i]["count"]),
                rx.button("+", on_click=PieChartState.increment(type_)),
            ),
        ),
    ),
    width="100%",
    height="15em",
)"""
```

```python eval
docgraphing(
    pie_chart_state_example,
    comp=eval(pie_chart_state_example),
    # data=inspect.getsource(PieChartState),
)
```

