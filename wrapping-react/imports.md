## 导入的基础知识

在决定通过包装组件来扩展 Reflex 之前，先检查是否有对应并且维护良好的 React 库。在 [npm](https://www.npmjs.com/) 上搜索，如果存在，就可以在 Reflex 应用中使用它。

```javascript 
import \{ HexColorPicker } from "react-colorful"
```

当包装一个 React 组件时，我们需要知道两个主要的事情：库和标签。

库是 npm 包的名称，而标签是 React 组件的名称。如上面的示例所示，库是 `react-colorful`，标签是 `HexColorPicker`。

对应的 Reflex 组件将如下所示：

```python
class ColorPicker(rx.Component):
    """Color picker component."""

    library = "react-colorful"
    tag = "HexColorPicker"
```

## 导入类型

如果标签是模块默认导出的，你可以在组件类中设置 `is_default = True`。这通常用于当导入组件时，它们在导入语句中没有大括号的情况。

我们在概述部分的 Spline 示例中可以看到这一点：

```javascript
import Spline from '@splinetool/react-spline';
```

要包装该组件，我们将在组件类中设置 `is_default = True`：

```python
class Spline(rx.Component):
    """Spline component."""
 
    library = "@splinetool/react-spline"
    tag = "Spline"
    scene: Var[str] = "https://prod.spline.design/Br2ec3WwuRGxEuij/scene.splinecode"
    is_default = True

    lib_dependencies: list[str] = ["@splinetool/runtime"]
```

## 库依赖

默认情况下，Reflex 会安装你在库属性中指定的库。但是，有时你可能需要安装其他库来使用一个组件。在这种情况下，你可以使用 `lib_dependencies` 属性来指定其他需要安装的库。

如在概述部分的 Spline 示例中所示，我们需要导入 `@splinetool/runtime` 库来使用 `Spline` 组件。我们可以在组件类中像这样指定：

```python
class Spline(rx.Component):
    """Spline component."""

    library = "@splinetool/react-spline"
    tag = "Spline"
    scene: Var[str] = "https://prod.spline.design/Br2ec3WwuRGxEuij/scene.splinecode"
    is_default = True

    lib_dependencies: list[str] = ["@splinetool/runtime"]
```

## 别名

如果你在项目中包装了与另一个组件具有相同标签的组件，你可以使用别名来区分它们，避免命名冲突。

让我们来看一下下面的代码，如果我们需要包装另一个带有相同标签的颜色选择器库，我们可以使用一个别名来避免冲突。

```python
class AnotherColorPicker(rx.Component):
    library = "some-other-colorpicker"
    tag = "HexColorPicker"
    alias = "OtherHexColorPicker"
    color: rx.Var[str]

    def get_event_triggers(self) -> dict[str, Any]:
        return \{
            **super().get_event_triggers(),
            "on_change": lambda e0: [e0],
        }
```

## 动态导入

有些你可能想要包装的库可能需要动态导入。这是因为它们可能与服务器端渲染（SSR）不兼容。

在 Reflex 中处理这个问题，你只需要在定义组件时将其作为 `NoSSRComponent` 的子类。

通常，当你看到类似下面这样的导入语句时：

```javascript
import dynamic from 'next/dynamic';

const MyLibraryComponent = dynamic(() => import('./MyLibraryComponent'), {
  ssr: false
});
```

你可以在 Reflex 中这样包装它，这里我们包装了需要动态导入的 `react-plotly.js` 库：

```python
from reflex.components.component import NoSSRComponent

class PlotlyLib(NoSSRComponent):
    """A component that wraps a plotly lib."""

    library = "react-plotly.js@2.6.0"

    lib_dependencies: List[str] = ["plotly.js@2.22.0"]
```

## 自定义代码

有时你可能需要向组件中添加自定义代码。这可以是任何内容，从添加自定义常量，到添加自定义导入，甚至添加自定义函数。自定义代码将被插入到 React 组件函数 _之外_。

```javascript
import React from "react";
// Other imports...
...

// Custom code
const customCode = "const customCode = 'customCode';";
```

要向组件添加自定义代码，你可以在组件类中使用 `get_custom_code` 方法。

```python
from reflex.components.component import NoSSRComponent

class PlotlyLib(NoSSRComponent):
    """A component that wraps a plotly lib."""

    library = "react-plotly.js@2.6.0"

    lib_dependencies: List[str] = ["plotly.js@2.22.0"]

    def _get_custom_code(self) -> str:
        return "const customCode = 'customCode';"
```

