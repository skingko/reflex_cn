---
components:
    - rx.recharts.LineChart
    - rx.recharts.Line
---

```python exec
import random
from typing import Any

import reflex as rx
from pcweb.templates.docpage import docgraphing

data = [
  {
    "name": "Page A",
    "uv": 4000,
    "pv": 2400,
    "amt": 2400
  },
  {
    "name": "Page B",
    "uv": 3000,
    "pv": 1398,
    "amt": 2210
  },
  {
    "name": "Page C",
    "uv": 2000,
    "pv": 9800,
    "amt": 2290
  },
  {
    "name": "Page D",
    "uv": 2780,
    "pv": 3908,
    "amt": 2000
  },
  {
    "name": "Page E",
    "uv": 1890,
    "pv": 4800,
    "amt": 2181
  },
  {
    "name": "Page F",
    "uv": 2390,
    "pv": 3800,
    "amt": 2500
  },
  {
    "name": "Page G",
    "uv": 3490,
    "pv": 4300,
    "amt": 2100
  }
]


line_chart_simple_example = """rx.recharts.line_chart(
                rx.recharts.line(
                    data_key="pv",
                    stroke="#8884d8",),
                rx.recharts.line(
                    data_key="uv",
                    stroke="#82ca9d",), 
                rx.recharts.x_axis(data_key="name"), 
                rx.recharts.y_axis(),
                data=data
                )"""

line_chart_complex_example = """rx.recharts.line_chart(
                rx.recharts.line(
                    data_key="pv",
                    type_="monotone",
                    stroke="#8884d8",),
                rx.recharts.line(
                    data_key="uv",
                    type_="monotone",
                    stroke="#82ca9d",), 
                rx.recharts.x_axis(data_key="name"), 
                rx.recharts.y_axis(),
                rx.recharts.cartesian_grid(stroke_dasharray="3 3"),
                rx.recharts.graphing_tooltip(),
                rx.recharts.legend(),
                data=data
                )"""
```

曲线图是一种用于展示随时间变化的信息的图表类型。曲线图通过绘制多个点并用直线连接它们来创建。

对于曲线图，我们需要为每组要绘制的值定义一个 `rx.recharts.line()` 组件。每个 `rx.recharts.line()` 组件有一个 `data_key`，它清楚地指出我们要跟踪的数据中的哪个变量。在这个简单的例子中，我们在 `rx.recharts.x_axis` 中将 `name` 列设置为 `data_key`，以分别绘制 `pv` 和 `uv` 两条线。

```python eval
docgraphing(line_chart_simple_example, comp=eval(line_chart_simple_example), data =  "data=" + str(data))
```

## 图表特点

我们的第二个示例使用与第一个示例完全相同的数据，只是现在我们给曲线图添加了一些额外的特征。我们给 `rx.recharts.line` 添加了一个 `type_` 属性以对线条进行样式设置。此外，我们添加了一个 `rx.recharts.cartesian_grid` 以获得背景网格，一个 `rx.recharts.legend` 以为图表添加一个图例，并且添加了一个 `rx.recharts.graphing_tooltip`，当鼠标指针停在图表中的某个元素上时，会出现一个带有文本的框。

```python eval
docgraphing(line_chart_complex_example, comp=eval(line_chart_complex_example), data =  "data=" + str(data))
```

## 动态数据和样式

```python exec
initial_data = data


class LineChartState(rx.State):
    data: list[dict[str, Any]] = initial_data
    pv_type: str = "monotone"
    uv_type: str = "monotone"

    def munge_data(self):
        for row in self.data:
            row["uv"] += random.randint(-500, 500)
            row["pv"] += random.randint(-1000, 1000)


line_chart_state_example = """rx.vstack(
                rx.recharts.line_chart(
                    rx.recharts.line(
                        data_key="pv",
                        type_=LineChartState.pv_type,
                        stroke="#8884d8",
                    ),
                    rx.recharts.line(
                        data_key="uv",
                        type_=LineChartState.uv_type,
                        stroke="#82ca9d",
                    ), 
                    rx.recharts.x_axis(data_key="name"), 
                    rx.recharts.y_axis(),
                    data=LineChartState.data,
                ),
                rx.button("Munge Data", on_click=LineChartState.munge_data),
                rx.select(
                    ["monotone", "linear", "step", "stepBefore", "stepAfter"],
                    value=LineChartState.pv_type,
                    on_change=LineChartState.set_pv_type
                ),
                rx.select(
                    ["monotone", "linear", "step", "stepBefore", "stepAfter"],
                    value=LineChartState.uv_type,
                    on_change=LineChartState.set_uv_type
                ),
                height="15em",
                width="100%",
            )"""
```

通过将 `data` 属性绑定到状态变量，可以修改图表数据。其他大多数属性，如 `type_`，也可以动态控制。在以下示例中，可以使用“混合数据”按钮随机修改数据，两个 `select` 元素改变线条的 `type_`。由于数据和样式保存在每个浏览器标签页的状态中，所以这些更改对其他访问者是不可见的。

```python eval
docgraphing(
    line_chart_state_example,
    comp=eval(line_chart_state_example),
    # data="initial_data=" + str(data) + "\n\n" + inspect.getsource(LineChartState),
)
```

