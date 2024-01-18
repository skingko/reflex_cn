```yaml
components:
    - rx.chakra.ButtonGroup
```

```python exec
import reflex as rx
from pcweb.templates.docpage import docdemo


basic_button_group = (
"""rx.button_group(
            rx.button('Option 1'),
            rx.button('Option 2'),
            rx.button('Option 3'),
        )
"""
)

button_group_attached = (
"""rx.button_group(
            rx.button('Option 1'),
            rx.button('Option 2'),
            rx.button('Option 3'),
            is_attached=True,
        )

"""  
)

button_group_variant = (
"""rx.button_group(
            rx.button('Option 1'),
            rx.button('Option 2'),
            rx.button('Option 3'),
            variant='ghost',
        )

"""  
)

button_group_sizes = (
"""rx.button_group(
            rx.button('Large Button', size='lg'),
            rx.button('Medium Button', size='md'),
            rx.button('Small Button', size='sm'),
        )

"""  
)

button_group_disable = (
"""rx.button_group(
            rx.button('Option 1'),
            rx.button('Option 2'),
            rx.button('Option 3'),
            is_disabled=True,
        )

"""  
)

button_group_spacing = (
"""rx.button_group(
            rx.button('Option 1'),
            rx.button('Option 2'),
            rx.button('Option 3'),
            spacing=8,
        )

"""  

)
```

# 按钮组

`rx.button_group` 组件允许您创建一组按钮，使它们在视觉上连接并共享样式。通常用于在应用程序的用户界面中将相关的操作或选项分组。

## 基本用法

以下是使用 `rx.button_group` 组件创建简单按钮组的示例：

```python eval
docdemo(basic_button_group)
```

在此示例中，创建了一个包含三个按钮的按钮组。这些按钮在视觉上连接，它们之间的默认间距为`2`像素。

## 调整 ButtonGroup 属性

您可以通过调整其属性来自定义 `rx.button_group` 组件的外观和行为。例如，您可以将 `is_attached` 属性设置为 `True`，使按钮看起来无缝连接在一起：

```python eval
docdemo(button_group_attached)
```

在此示例中，将 `is_attached` 属性设置为 `True`，使按钮具有无缝连接的外观。

## ButtonGroup 变体

与 `button` 组件一样，您可以使用 `variant` 属性自定义按钮的视觉样式。这将应用于组内的所有按钮。

```python eval
docdemo(button_group_variant)
```

在此示例中，将 `variant` 属性设置为 `ghost`，将变体样式应用于组内的所有按钮。

## ButtonGroup 大小

类似地，您可以使用 `size` 属性调整按钮组内按钮的大小。此属性允许您选择不同的尺寸选项，从而影响组内的所有按钮。

```python eval
docdemo(button_group_sizes)
```

在此示例中，使用 `size` 属性设置了组内所有按钮的大小，可选择的选项有 `"lg"`（大）、`"md"`（中）和 `"sm"`（小）。

## 禁用 ButtonGroup

您还可以通过将 `is_disabled` 属性设置为 `True` 禁用按钮组内的所有按钮：

```python eval
docdemo(button_group_disable)
```

在这种情况下，组内的所有按钮都将被禁用且无法点击。

## 自定义间距

`spacing` 属性允许您控制组内按钮之间的间距。以下是设置自定义间距为`8`像素的示例：

```python eval
docdemo(button_group_spacing)
```

通过将 `spacing` 设置为 `8`，按钮之间将有更大的间隔。

```md alert info
- You can nest other components or elements within the button group to create more complex layouts.
- Button groups are a useful way to visually organize related actions or options in your application, providing a consistent and cohesive user interface.
- Experiment with different combinations of props to achieve the desired styling and behavior for your button groups in Reflex-based applications.
```
```

