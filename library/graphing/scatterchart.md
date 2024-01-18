---

components:
    - rx.recharts.ScatterChart
    - rx.recharts.Scatter
---

```python exec
import reflex as rx
from pcweb.templates.docpage import docgraphing

data01 = [
  {
    "x": 100,
    "y": 200,
    "z": 200
  },
  {
    "x": 120,
    "y": 100,
    "z": 260
  },
  {
    "x": 170,
    "y": 300,
    "z": 400
  },
  {
    "x": 170,
    "y": 250,
    "z": 280
  },
  {
    "x": 150,
    "y": 400,
    "z": 500
  },
  {
    "x": 110,
    "y": 280,
    "z": 200
  }
]

data02 = [
  {
    "x": 200,
    "y": 260,
    "z": 240
  },
  {
    "x": 240,
    "y": 290,
    "z": 220
  },
  {
    "x": 190,
    "y": 290,
    "z": 250
  },
  {
    "x": 198,
    "y": 250,
    "z": 210
  },
  {
    "x": 180,
    "y": 280,
    "z": 260
  },
  {
    "x": 210,
    "y": 220,
    "z": 230
  }
]

scatter_chart_simple_example = """rx.recharts.scatter_chart(
                rx.recharts.scatter(
                    data=data01,
                    fill="#8884d8",),
                rx.recharts.x_axis(data_key="x", type_="number"), 
                rx.recharts.y_axis(data_key="y")
                )"""

scatter_chart_simple_complex = """rx.recharts.scatter_chart(
                rx.recharts.scatter(
                    data=data01,
                    fill="#8884d8",
                    name="A"
                  ),
                rx.recharts.scatter(
                    data=data02,
                    fill="#82ca9d",
                    name="B"
                  ),
                rx.recharts.cartesian_grid(stroke_dasharray="3 3"),
                rx.recharts.x_axis(data_key="x", type_="number"), 
                rx.recharts.y_axis(data_key="y"),
                rx.recharts.z_axis(data_key="z", range=[60, 400], name="score"),
                rx.recharts.legend(),
                rx.recharts.graphing_tooltip(),
                
                )"""

```

散点图通常有两个数值轴，其中一个水平轴显示一组数值数据，另一个垂直轴显示另一组数值数据。该图在 x 和 y 数值值的交叉点显示点，将这些值组合成单个数据点。

对于散点图，我们必须为要绘制的每组值定义一个 `rx.recharts.scatter()` 组件。每个 `rx.recharts.scatter()` 组件都有一个 `data` 属性，明确指定了要绘制的数据源。我们还必须定义 `rx.recharts.x_axis()` 和 `rx.recharts.y_axis()`，以使图表知道在每个轴上绘制哪些数据。

```python eval
docgraphing(scatter_chart_simple_example, comp=eval(scatter_chart_simple_example), data =  "data01=" + str(data01))
```

我们还可以通过使用两个 `rx.recharts.scatter()` 组件在一个图表上添加两个散点，并且我们可以定义一个 `rx.recharts.z_axis()`，它表示第三列数据，并由散点图中点的大小表示。

```python eval
docgraphing(scatter_chart_simple_complex, comp=eval(scatter_chart_simple_complex), data =  "data01=" + str(data01) + "&data02=" + str(data02))
```

# 动态数据


与状态变量绑定的图表会在状态发生变化时自动更新，这是一种很好的方式，可以根据用户界面元素来可视化数据。查看 "Data" 选项卡以查看驱动此计算的子状态，用于给定初始数字的 Collatz 猜想中的迭代。在图表下方的框中输入一个起始数字进行重新计算。

```python demo graphing
class ScatterChartState(rx.State):
    data: list[dict[str, int]] = []

    def compute_collatz(self, form_data: dict) -> int:
        n = int(form_data["start"])
        yield rx.set_value("start", "")
        self.data = []
        for ix in range(400):
            self.data.append({"x": ix, "y": n})
            if n == 1:
                break
            if n % 2 == 0:
                n = n // 2
            else:
                n = 3 * n + 1


def index():
    return rx.vstack(
        rx.recharts.scatter_chart(
            rx.recharts.scatter(
                data=ScatterChartState.data,
                fill="#8884d8",
            ),
            rx.recharts.x_axis(data_key="x", type_="number"),
            rx.recharts.y_axis(data_key="y", type_="number"),
        ),
        rx.form(
            rx.input(placeholder="Enter a number", id="start"),
            rx.button("Compute", type_="submit"),
            on_submit=ScatterChartState.compute_collatz,
        ),
        width="100%",
        height="15em",
        on_mount=ScatterChartState.compute_collatz({"start": "15"}),
    )
```

