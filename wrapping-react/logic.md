## 声明变量

如我们在 [state section](https://reflex.dev/docs/state/) 中所见，我们可以使用 `rx.Var` 在 Reflex 应用程序中定义状态变量。

当包装自己的 React 组件时，您可以使用 `rx.Var` 来定义组件的 props。在下面的示例中，我们为我们的 `ColorPicker` 组件定义了一个 `color` 属性。

```python
class ColorPicker(rx.Component):
    library = "react-colorful"
    tag = "HexColorPicker"
    color: rx.Var[str]
```

然而，变量不仅可以是一个简单类型。您的变量可以是任意组合的基本类型。

```python
class SomeComponent(rx.Component):

    tag = "SomeComponent"

    data: Var[List[Dict[str, Any]]]
```

在这里，我们定义了一个变量，它是一个字典列表。这对于想要向组件传递一组数据非常有用。

## 序列化变量

有时您可能希望创建一个不是常见的基本类型的变量。在这种情况下，您可以使用 `serializer` 将变量转换为可以存储在状态中的基本类型。

下面是一个例子，演示了如何将一个 plotly 图表序列化为可以存储在状态中的 json。

```python
import json
from typing import Any, Dict, List

from reflex.components.component import NoSSRComponent
from reflex.utils.serializers import serializer
from reflex.vars import Var

try:
    from plotly.graph_objects import Figure
except ImportError:
    Figure = Any
    
class PlotlyLib(NoSSRComponent):
    """A component that wraps a plotly lib."""

    library = "react-plotly.js@2.6.0"

    lib_dependencies: List[str] = ["plotly.js@2.22.0"]


class Plotly(PlotlyLib):
    """Display a plotly graph."""

    tag = "Plot"

    is_default = True

    # The figure to display. This can be a plotly figure or a plotly data json.
    data: Var[Figure]

    ...


try:
    from plotly.graph_objects import Figure
    from plotly.io import to_json

    @serializer
    def serialize_figure(figure: Figure) -> list:
        """Serialize a plotly figure.

        Args:
            figure: The figure to serialize.

        Returns:
            The serialized figure.
        """
        return json.loads(str(to_json(figure)))["data"]

except ImportError:
    pass
```

## 事件触发器

如我们在 [events section](https://reflex.dev/docs/state/events/) 中所见，我们可以使用事件触发器来处理 Reflex 应用程序中的事件。当包装自己的 React 组件时，您可以使用 `get_event_triggers` 方法为组件定义事件触发器。

有时这些事件触发器可能需要参数，例如，在我们在 [wrapping react section](https://reflex.dev/docs/wrapping-react/wrapping-react/) 中看到的 `HexColorPicker` 组件的 `on_change` 事件触发器。在这种情况下，我们可以使用 lambda 函数将事件参数传递给事件触发器。与触发器关联的函数将把 JavaScript 触发器的 args 映射到将传递给后端事件处理函数的 args。

```python
class ColorPicker(rx.Component):
    library = "react-colorful"
    tag = "HexColorPicker"
    color: rx.Var[str]

    def get_event_triggers(self) -> dict[str, Any]:
        return \{
            **super().get_event_triggers(),
            "on_change": lambda e0: [e0],
        }
```

