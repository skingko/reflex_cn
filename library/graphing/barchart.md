---
components:
    - rx.recharts.BarChart
    - rx.recharts.RadialBarChart
    - rx.recharts.Bar
---

```python exec
import reflex as rx
from pcweb.templates.docpage import docdemo, docgraphing
import random

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

range_data = [
  {
    "day": "05-01",
    "temperature": [
      -1,
      10
    ]
  },
  {
    "day": "05-02",
    "temperature": [
      2,
      15
    ]
  },
  {
    "day": "05-03",
    "temperature": [
      3,
      12
    ]
  },
  {
    "day": "05-04",
    "temperature": [
      4,
      12
    ]
  },
  {
    "day": "05-05",
    "temperature": [
      12,
      16
    ]
  },
  {
    "day": "05-06",
    "temperature": [
      5,
      16
    ]
  },
  {
    "day": "05-07",
    "temperature": [
      3,
      12
    ]
  },
  {
    "day": "05-08",
    "temperature": [
      0,
      8
    ]
  },
  {
    "day": "05-09",
    "temperature": [
      -3,
      5
    ]
  }
]

bar_chart_state = """class BarState(rx.State):
    data=data

    def randomize_data(self):
        for i in range(len(self.data)):
            self.data[i]["uv"] = random.randint(0, 10000)
            self.data[i]["pv"] = random.randint(0, 10000)
            self.data[i]["amt"] = random.randint(0, 10000)


"""
exec(bar_chart_state)

bar_chart_example = """rx.recharts.bar_chart(
                rx.recharts.bar(
                    data_key="uv",
                    stroke="#8884d8",
                    fill="#8884d8"
                ), 
                rx.recharts.x_axis(data_key="name"), 
                rx.recharts.y_axis(),
                data=data)"""

bar_chart_example_2 = """rx.recharts.bar_chart(
                rx.recharts.bar(
                    data_key="uv",
                    stroke="#8884d8",
                    fill="#8884d8"
                ), 
                rx.recharts.bar(
                    data_key="pv",
                    stroke="#82ca9d",
                    fill="#82ca9d"
                ), 
                rx.recharts.x_axis(data_key="name"), 
                rx.recharts.y_axis(),
                data=data)"""


range_bar_chart = """rx.recharts.bar_chart(
                rx.recharts.bar(
                    data_key="temperature",
                    stroke="#8884d8",
                    fill="#8884d8"
                ), 
                rx.recharts.x_axis(data_key="day"), 
                rx.recharts.y_axis(),
                data=range_data)"""

bar_chart_example_with_state = """rx.recharts.bar_chart(
            rx.recharts.bar(
                data_key="uv",
                stroke="#8884d8",
                fill="#8884d8",
                type_="natural",
                on_click=BarState.randomize_data,

            ),
            rx.recharts.bar(
                data_key="pv",
                stroke="#82ca9d", 
                fill="#82ca9d",
                type_="natural",
            ),
            rx.recharts.x_axis(
                data_key="name",
            ),
            rx.recharts.y_axis(), 
            rx.recharts.legend(),
            rx.recharts.cartesian_grid(
                stroke_dasharray="3 3",
            ),
            data=BarState.data,
            width="100%",
            height=400,
        ) 
"""
```


柱状图用高度或长度与其所代表的值成比例的矩形条来展示分类数据。

对于柱状图，我们必须为每组要绘制的值定义一个 `rx.recharts.bar()` 组件。每个 `rx.recharts.bar()` 组件都有一个 `data_key`，清楚地指明了我们要跟踪的数据中的哪个变量。在这个简单的示例中，我们将 `uv` 以柱状图形式绘制，并将 `name` 列设置为 `rx.recharts.x_axis` 中的 `data_key`。


```python eval
docgraphing(
  bar_chart_example, 
  comp = eval(bar_chart_example),
  data =  "data=" + str(data)
)
```

可以使用多个 `rx.recharts.bar()` 组件将多个柱状图放置在同一个 `bar_chart` 上。

```python eval
docgraphing(
  bar_chart_example_2, 
  comp = eval(bar_chart_example_2),
  data =  "data=" + str(data)
)
```

您还可以通过将 `rx.recharts.bar` 中的 `data_key` 分配给一个包含两个元素的列表来为柱形图分配范围，比如在这里为每个日期分配了两个温度的范围。

```python eval
docgraphing(
  range_bar_chart, 
  comp = eval(range_bar_chart),
  data =  "data=" + str(range_data)
)
```

这是一个带有 `State` 的柱状图示例。在这里，我们定义了一个名为 `randomize_data` 的函数，当点击第一个定义的 `bar` 时，它会随机更改两个图表的数据，使用 `on_click=BarState.randomize_data`。

```python eval
docdemo(bar_chart_example_with_state,
        state=bar_chart_state,
        comp=eval(bar_chart_example_with_state),
        context=True,
)
```

