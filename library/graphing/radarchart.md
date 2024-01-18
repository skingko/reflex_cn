---

components:
- rx.recharts.RadarChart
---

```python exec
import reflex as rx
from pcweb.templates.docpage import docgraphing

data = [
  {
    "subject": "Math",
    "A": 120,
    "B": 110,
    "fullMark": 150
  },
  {
    "subject": "Chinese",
    "A": 98,
    "B": 130,
    "fullMark": 150
  },
  {
    "subject": "English",
    "A": 86,
    "B": 130,
    "fullMark": 150
  },
  {
    "subject": "Geography",
    "A": 99,
    "B": 100,
    "fullMark": 150
  },
  {
    "subject": "Physics",
    "A": 85,
    "B": 90,
    "fullMark": 150
  },
  {
    "subject": "History",
    "A": 65,
    "B": 85,
    "fullMark": 150
  }
]

radar_chart_simple_example = """rx.recharts.radar_chart(
                rx.recharts.radar(
                    data_key="A",
                    stroke="#8884d8",
                    fill="#8884d8",
                    ),
                    rx.recharts.polar_grid(),
                    rx.recharts.polar_angle_axis(data_key="subject"),
                    data=data
                    )"""

radar_chart_complex_example = """rx.recharts.radar_chart(
                rx.recharts.radar(
                    data_key="A",
                    stroke="#8884d8",
                    fill="#8884d8",
                    ),
                rx.recharts.radar(
                    data_key="B",
                    stroke="#82ca9d",
                    fill="#82ca9d",
                    fill_opacity=0.6,
                    ),
                    rx.recharts.polar_grid(),
                    rx.recharts.polar_angle_axis(data_key="subject"),
                    rx.recharts.legend(),
                    data=data
                    )"""

```

雷达图显示了三个或更多数量型变量映射到轴上的多变量数据。

对于雷达图，我们必须为每组要绘制的值定义一个`rx.recharts.radar()`组件。每个`rx.recharts.radar()`组件都有一个`data_key`，用于明确表示我们正在绘制的数据中的哪个变量。在这个简单的例子中，我们将数据的`A`列与`subject`列进行绘制，将其设置为`rx.recharts.polar_angle_axis`的`data_key`。


```python eval
docgraphing(radar_chart_simple_example, comp=eval(radar_chart_simple_example),  data =  "data=" + str(data))
```

我们还可以通过使用两个`rx.recharts.radar`组件在一个图表上添加两个雷达图。

```python eval
docgraphing(radar_chart_complex_example, comp=eval(radar_chart_complex_example),  data =  "data=" + str(data))
```

# 动态数据

与状态变量相关联的图表数据会在状态改变时自动更新，这提供了一种很好的方式来根据用户界面元素可视化数据。浏览“数据”选项卡以查看驱动这个特征雷达图的子状态。

```python exec
from typing import Any


class RadarChartState(rx.State):
    total_points: int = 100
    traits: list[dict[str, Any]] = [
        dict(trait="Strength", value=15),
        dict(trait="Dexterity", value=15),
        dict(trait="Constitution", value=15),
        dict(trait="Intelligence", value=15),
        dict(trait="Wisdom", value=15),
        dict(trait="Charisma", value=15),
    ]

    @rx.var
    def remaining_points(self) -> int:
        return self.total_points - sum(t["value"] for t in self.traits)

    @rx.cached_var
    def trait_names(self) -> list[str]:
        return [t["trait"] for t in self.traits]

    def set_trait(self, trait: str, value: int):
        for t in self.traits:
            if t["trait"] == trait:
                available_points = self.remaining_points + t["value"]
                value = min(value, available_points)
                t["value"] = value
                break

radar_chart_state_example = """
rx.hstack(
    rx.recharts.radar_chart(
        rx.recharts.radar(
            data_key="value",
            stroke="#8884d8",
            fill="#8884d8",
        ),
        rx.recharts.polar_grid(),
        rx.recharts.polar_angle_axis(data_key="trait"),
        data=RadarChartState.traits,
    ),
    rx.vstack(
        rx.foreach(
            RadarChartState.trait_names,
            lambda trait_name, i: rx.hstack(
                rx.text(trait_name, width="7em"),
                rx.slider(
                    value=RadarChartState.traits[i]["value"].to(int),
                    on_change=lambda value: RadarChartState.set_trait(trait_name, value),
                    width="25vw",
                ),
                rx.text(RadarChartState.traits[i]['value']),
            ),
        ),
        rx.text("Remaining points: ", RadarChartState.remaining_points),
    ),
    width="100%",
    height="15em",
)
"""
```

```python eval
docgraphing(
    radar_chart_state_example,
    comp=eval(radar_chart_state_example),
    # data=inspect.getsource(RadarChartState),
)
```

