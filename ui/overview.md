```python exec
from pcweb.pages.docs import components
from pcweb.pages.docs.library import library
import reflex as rx
```

# UI 概览

组件是应用程序用户界面 (UI) 的构建块。它们是构成应用程序的可视元素，例如按钮、文本和图像。

## 组件基础知识

组件由子组件和属性 (props) 组成。

```md definition
# Children
* Text or other Reflex components nested inside a component.
* Passed as **positional arguments**.

# Props
* Attributes that affect the behavior and appearance of a component.
* Passed as **keyword arguments**.
```

让我们来看一下 `rx.text` 组件。

```python demo
rx.text('Hello World!', color='blue', font_size="1.5em")
```

这里的 `"Hello World!"` 是要显示的子文本，而 `color` 和 `font_size` 是修改文本外观的属性。

```md alert success
Regular Python data types can be passed in as children to components.
This is useful for passing in text, numbers, and other simple data types.
```

## 另一个例子

现在让我们来看一个更复杂的组件，该组件内部嵌套有其他组件。`rx.hstack` 组件是一个容器，它将其子组件在水平方向上排列。

```python demo
rx.hstack(
    # Static 50% progress
    rx.circular_progress(
        rx.circular_progress_label("50", color="green"),
        value=50,
    ),
    # "Spinning" progress
    rx.circular_progress(
        rx.circular_progress_label("∞", color="rgb(107,99,246)"),
        is_indeterminate=True,
    ),
)
```

某些属性是特定于某个组件的。例如，`rx.circular_progress` 组件的 `value` 属性控制进度条的值。

而像 `color` 这样的样式属性则共享给许多组件使用。

```md alert info
# You can find all the props for a component by checking its documentation page in the [component library]({library.path}).
```

## 页面

Reflex 应用程序按页面组织。页面将特定的 URL 路由链接到一个组件。

您可以通过定义一个返回组件的函数来创建一个页面。默认情况下，函数名将用作路径，但您也可以显式指定路径。

```python
def index():
    return rx.text('Root Page')


def about():
    return rx.text('About Page')


app = rx.App()
app.add_page(index, route="/")
app.add_page(about, route="/about")
```

在本例中，我们在根路由上添加了一个名为 `index` 的页面。如果您运行 `reflex run` 来启动应用程序，您将在 `http://localhost:3000` 上看到 `index` 页面。同样，`about` 页面将在 `http://localhost:3000/about` 上可用。

