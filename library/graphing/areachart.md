---

components:
    - rx.recharts.AreaChart
    - rx.recharts.Area
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


area_chart_state = """class AreaState(rx.State):
    data=data

    def randomize_data(self):
        for i in range(len(self.data)):
            self.data[i]["uv"] = random.randint(0, 10000)
            self.data[i]["pv"] = random.randint(0, 10000)
            self.data[i]["amt"] = random.randint(0, 10000)


"""
exec(area_chart_state)


area_chart_example = """rx.recharts.area_chart(
                rx.recharts.area(
                    data_key="uv",
                    stroke="#8884d8",
                    fill="#8884d8"
                ), 
                rx.recharts.x_axis(data_key="name"), 
                rx.recharts.y_axis(),
                data=data)"""

area_chart_example_2 = """rx.recharts.area_chart(
                rx.recharts.area(
                    data_key="uv",
                    stroke="#8884d8",
                    fill="#8884d8"
                ), 
                rx.recharts.area(
                    data_key="pv",
                    stroke="#82ca9d",
                    fill="#82ca9d"
                ), 
                rx.recharts.x_axis(data_key="name"), 
                rx.recharts.y_axis(),
                data=data)"""


range_area_chart = """rx.recharts.area_chart(
                rx.recharts.area(
                    data_key="temperature",
                    stroke="#8884d8",
                    fill="#8884d8"
                ), 
                rx.recharts.x_axis(data_key="day"), 
                rx.recharts.y_axis(),
                data=range_data)"""


area_chart_example_with_state = """rx.recharts.area_chart(
            rx.recharts.area(
                data_key="uv",
                stroke="#8884d8",
                fill="#8884d8",
                type_="natural",
                on_click=AreaState.randomize_data,

            ),
            rx.recharts.area(
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
            data=AreaState.data,
            width="100%",
            height=400,
        ) 
"""
```

面积图将折线图和柱状图结合在一起，展示一个或多个组的数值随第二个变量（通常是时间）的变化情况。与折线图相比，面积图通过在线条之间添加阴影和基线来区分出来，就像柱状图一样。

对于面积图，我们需要定义一个 `rx.recharts.area()` 组件，该组件具有一个 `data_key`，清楚地说明我们正在追踪的数据的变量是什么。在这个简单的示例中，我们追踪的是 `uv` 相对于 `name` 的变化，因此将 `rx.recharts.x_axis` 设置为 `name`。

```python eval
docgraphing(
  area_chart_example, 
  comp = eval(area_chart_example),
  data =  "data=" + str(data)
)
```

多个面积图可以放置在同一个 `area_chart` 上。

```python eval
docgraphing(
  area_chart_example_2, 
  comp = eval(area_chart_example_2),
  data =  "data=" + str(data)
)
```

您还可以通过将 `rx.recharts.area` 中的 `data_key` 分配给一个包含两个元素的列表来指定面积的范围，例如在这里为每个日期指定了两个温度的范围。

```python eval
docgraphing(
  area_chart_example_2, 
  comp = eval(range_area_chart),
  data =  "data=" + str(range_data)
)
```

这是一个带有 `State` 的面积图示例。在这里，我们定义了一个函数 `randomize_data`，当点击第一个定义的 `area` 时，可以随机更改两个图表的数据，方法是使用 `on_click=AreaState.randomize_data` 。

```python eval
docdemo(area_chart_example_with_state,
        state=area_chart_state,
        comp=eval(area_chart_example_with_state),
        context=True,
)
```

