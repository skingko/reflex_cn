```python exec
import reflex as rx
from typing import Any
from pcweb.components.spline import spline
from pcweb.templates.docpage import demo_box_style
```
# Reflex 概述


Reflex 最强大的功能之一是能够包装 React 组件。这使我们能够构建在现有的 React 生态系统基础上，并利用现有的 React 组件和库。

如果你想要一个特定的组件用于你的应用程序，但 Reflex 并没有提供，很有可能这个组件作为一个 React 组件存在。在 [npm](https://www.npmjs.com/) 上搜索一下，如果有的话，就可以在你的 Reflex 应用程序中使用。

在本节中，我们将概述如何在高层次上包装 React 组件。在接下来的几节中，我们将详细介绍如何包装更复杂的组件。


## Spline 示例


让我们从一个名为 [Spline](https://spline.design/) 的库开始。Spline 是一个用于创建 3D 场景和动画的工具。它是一个非常好的工具，用于创建交互式的 3D 可视化效果。


我们有一些用于创建 Spline 场景的 React 代码。我们希望将这个代码包装成一个 Reflex 组件，以便在 Reflex 应用程序中使用。

```javascript
import Spline from '@splinetool/react-spline';

export default function App() {
  return (
    <Spline scene="https://prod.spline.design/up1SQcRLq1s6yks3/scene.splinecode" />
  );
}
```
以下是如何在 Reflex 中包装这个组件。

最重要的两个属性是 `library`，它是 npm 包的名称，以及 `tag`，它是 React 组件的名称。

```python
class Spline(rx.Component):
    """Spline component."""

    library = "@splinetool/react-spline"
    tag = "Spline"
    scene: Var[str] = "https://prod.spline.design/Br2ec3WwuRGxEuij/scene.splinecode"
    is_default = True

    lib_dependencies: list[str] = ["@splinetool/runtime"]
```


这里的 library 是 `@splinetool/react-spline`，tag 是 `Spline`。在下一节中，我们将对导入进行深入讲解，但是我们也将 `is_default = True` 设置为 True，因为 tag 是模块的默认导出。

此外，我们还可以指定组件接受的任何属性。在这种情况下，`Spline` 组件接受一个 `scene` 属性，它是 Spline 场景的 URL。


## 完整示例

```python eval
rx.center(
        spline(
            scene="https://prod.spline.design/joLpOOYbGL-10EJ4/scene.splinecode"
        ),
        overflow="hidden",
        width="100%",
        height="30em",
        padding="0",
        margin_bottom="1em",
        style=demo_box_style,
    )
```

```python
class Spline(rx.Component):
    """Spline component."""

    library = "@splinetool/react-spline"
    tag = "Spline"
    scene: Var[str] ="https://prod.spline.design/joLpOOYbGL-10EJ4/scene.splinecode"
    is_default = True

    lib_dependencies: list[str] = ["@splinetool/runtime"]

spline = Spline.create

def spline_example():
    return rx.center(
        spline(),
        overflow="hidden",
        width="100%",
        height="30em",
    )
```

## ColorPicker 示例

与 Spline 示例类似，我们首先定义库和标签。在本例中，库是 `react-colorful`，标签是 `HexColorPicker`。

我们还有一个 `color` 变量，它是颜色选择器的当前颜色。

由于此组件具有交互功能，我们必须指定组件接受的任何事件触发器。颜色选择器有一个触发器 `on_change`，用于指定颜色何时变化。此触发器接受一个参数 `color`，它是新的颜色。在这里，`super().get_event_triggers()` 用于获取所有组件的默认事件触发器。


```python exec
class ColorPicker(rx.Component):
    library = "react-colorful"
    tag = "HexColorPicker"
    color: rx.Var[str]

    def get_event_triggers(self) -> dict[str, Any]:
        return {
            **super().get_event_triggers(),
            "on_change": lambda e0: [e0],
        }

color_picker = ColorPicker.create


class ColorPickerState(rx.State):
    color: str = "#db114b"
```

```python eval
rx.box(
        rx.vstack(
            rx.heading(ColorPickerState.color, color="white"),
            color_picker(
                on_change=ColorPickerState.set_color
            ),
        ),
        background_color=ColorPickerState.color,
        padding="5em",
        border_radius="1em",
        margin_bottom="1em",
    )
```

```python
class ColorPicker(rx.Component):
    library = "react-colorful"
    tag = "HexColorPicker"
    color: rx.Var[str]

    def get_event_triggers(self) -> dict[str, Any]:
        return \{
            **super().get_event_triggers(),
            "on_change": lambda e0: [e0],
        \}

color_picker = ColorPicker.create

class ColorPickerState(rx.State):
    color: str = "#db114b"

def index():
    return rx.box(
        rx.vstack(
            rx.heading(ColorPickerState.color, color="white"),
            color_picker(
                on_change=ColorPickerState.set_color
            ),
        ),
        background_color=ColorPickerState.color,
        padding="5em",
        border_radius="1em",
    )

```

