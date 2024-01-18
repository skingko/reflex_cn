---
components:
    - rx.chakra.Button
    - rx.chakra.IconButton
---

```python exec
import reflex as rx
from pcweb.templates.docpage import docdemo


basic_button = """rx.button("Click Me!")
"""
button_style = """rx.button_group(
    rx.button("Example", bg="lightblue", color="black", size = 'sm'),
    rx.button("Example", bg="orange", color="white", size = 'md'),
    rx.button("Example", color_scheme="red", size = 'lg'),
    space = "1em",
)
"""
button_visual_states = """rx.button_group(
    rx.button("Example", bg="lightgreen", color="black", is_loading = True),
    rx.button("Example", bg="lightgreen", color="black", is_disabled = True),
    rx.button("Example", bg="lightgreen", color="black", is_active = True),
    space = '1em',
)
"""

button_group_example = """rx.button_group(
    rx.button(rx.icon(tag="minus"), color_scheme="red"),
    rx.button(rx.icon(tag="add"), color_scheme="green"),
    is_attached=True,
)
"""

button_state = """class ButtonState(rx.State):
    count: int = 0

    def increment(self):
        self.count += 1

    def decrement(self):
        self.count -= 1
"""
exec(button_state)
button_state_example = """rx.hstack(
    rx.button(
        "Decrement",
        bg="#fef2f2",
        color="#b91c1c",
        border_radius="lg",
        on_click=ButtonState.decrement,
    ),
    rx.heading(ButtonState.count, font_size="2em", padding_x="0.5em"),
    rx.button(
        "Increment",
        bg="#ecfdf5",
        color="#047857",
        border_radius="lg",
        on_click=ButtonState.increment,
    ),
)
"""


button_state_code = f"""
import reflex as rx

{button_state}

def index():
    return {button_state_example}

app = rx.App()
app.add_page(index)
app.compile()"""

button_state2 = """class ExampleButtonState(rx.State):
    text_value: str = "Random value"
"""
exec(button_state2)

button_state2_render_code = """rx.vstack(
	rx.text(ExampleButtonState.text_value),
        rx.button(
            "Change Value",
            on_click=ExampleButtonState.set_text_value("Modified value"))
    )
"""

button_state2_code = f"""
import reflex as rx

{button_state2}

def index():
    return {button_state2_render_code}

app = rx.App()
app.add_page(index)
app.compile()"""


button_sizes = (
"""rx.button_group(
        rx.button(
        'Example', bg='lightblue', color='black', size='sm'
        ),
        rx.button(
            'Example', bg='orange', color='white', size='md'
        ),
        rx.button('Example', color_scheme='red', size='lg'),
)
"""  
)

button_colors = (
"""rx.button_group(
        rx.button('White Alpha', color_scheme='whiteAlpha', min_width='unset'),
        rx.button('Black Alpha', color_scheme='blackAlpha', min_width='unset'),
        rx.button('Gray', color_scheme='gray', min_width='unset'),
        rx.button('Red', color_scheme='red', min_width='unset'),
        rx.button('Orange', color_scheme='orange', min_width='unset'),
        rx.button('Yellow', color_scheme='yellow', min_width='unset'),
        rx.button('Green', color_scheme='green', min_width='unset'),
        rx.button('Teal', color_scheme='teal', min_width='unset'),
        rx.button('Blue', color_scheme='blue', min_width='unset'),
        rx.button('Cyan', color_scheme='cyan', min_width='unset'),
        rx.button('Purple', color_scheme='purple', min_width='unset'),
        rx.button('Pink', color_scheme='pink', min_width='unset'),
        rx.button('LinkedIn', color_scheme='linkedin', min_width='unset'),
        rx.button('Facebook', color_scheme='facebook', min_width='unset'),
        rx.button('Messenger', color_scheme='messenger', min_width='unset'),
        rx.button('WhatsApp', color_scheme='whatsapp', min_width='unset'),
        rx.button('Twitter', color_scheme='twitter', min_width='unset'),
        rx.button('Telegram', color_scheme='telegram', min_width='unset'),
        width='100%',
)

""" 
)

button_colors_render_code = (
"""rx.button_group(
        rx.button('White Alpha', color_scheme='whiteAlpha'),
        rx.button('Black Alpha', color_scheme='blackAlpha'),
        rx.button('Gray', color_scheme='gray'),
        rx.button('Red', color_scheme='red'),
        rx.button('Orange', color_scheme='orange'),
        rx.button('Yellow', color_scheme='yellow'),
        rx.button('Green', color_scheme='green'),
        rx.button('Teal', color_scheme='teal'),
        rx.button('Blue', color_scheme='blue'),
        rx.button('Cyan', color_scheme='cyan'),
        rx.button('Purple', color_scheme='purple'),
        rx.button('Pink', color_scheme='pink'),
        rx.button('LinkedIn', color_scheme='linkedin'),
        rx.button('Facebook', color_scheme='facebook'),
        rx.button('Messenger', color_scheme='messenger'),
        rx.button('WhatsApp', color_scheme='whatsapp'),
        rx.button('Twitter', color_scheme='twitter'),
        rx.button('Telegram', color_scheme='telegram'),
)

""" 
)

button_variants = (
"""rx.button_group(
        rx.button('Ghost Button', variant='ghost'),
        rx.button('Outline Button', variant='outline'),
        rx.button('Solid Button', variant='solid'),
        rx.button('Link Button', variant='link'),
        rx.button('Unstyled Button', variant='unstyled'),
    )
"""  

)

button_disable = (
"""rx.button('Inactive button', is_disabled=True)"""  
)
  
loading_states = (
"""rx.button(
            'Random button',
            is_loading=True,
            loading_text='Loading...',
            spinner_placement='start'
    )
"""  
)

stack_buttons_vertical = (
"""rx.stack(
        rx.button('Button 1'),
        rx.button('Button 2'),
        rx.button('Button 3'),
        direction='column',
)

"""  
)

stack_buttons_horizontal = (
"""rx.stack(
        rx.button('Button 1'),
        rx.button('Button 2'),
        rx.button('Button 3'),
        direction='row',
)
"""  
)

button_group = (
"""rx.button_group(
            rx.button('Option 1'),
            rx.button('Option 2'),
            rx.button('Option 3'),
            variant='outline',
	        is_attached=True,
        )
"""  

)

```
# 按钮

按钮是应用程序用户界面中的重要元素，用户可以单击它们来触发事件。此文档将帮助您了解如何在 Reflex 应用程序中有效使用按钮组件。

## 基本用法
使用 `rx.button` 方法可以创建基本的按钮组件：

```python eval
docdemo(basic_button)
```
## 按钮大小
您可以通过将大小属性设置为以下值之一来更改按钮的大小：`xs`,`sm`,`md` 或 `lg`。

```python eval
docdemo(button_sizes)
```

## 按钮颜色
通过调整颜色方案属性来自定义按钮的外观。您可以灵活选择设计系统提供的一系列颜色比例尺，例如 whiteAlpha、blackAlpha、gray、red、blue，甚至可以使用自定义的颜色比例尺。

```python demo box
eval(button_colors)
```

```python
{button_colors_render_code.strip()}
```

## 按钮变体
您可以使用变体属性自定义按钮的视觉样式。以下是可用的按钮变体：
- `ghost`：具有透明背景和可见文本的按钮。
- `outline`：没有背景颜色，但有边框的按钮。
- `solid`：具有实心背景颜色的默认按钮样式。
- `link`：类似于文本链接的按钮。
- `unstyled`：没有特定样式的按钮。

```python eval
docdemo(button_variants)
```
## 禁用按钮
通过将 `is_disabled` 属性设置为 `True`，可以使按钮无效。

```python eval
docdemo(button_disable)
```

## 处理加载状态
为了在按钮被单击后显示加载状态，您可以使用以下属性：
- `is_loading`：将此属性设置为 `True` 以显示加载旋转器。
- `loading_text`：可选地，可以提供加载文本以与旋转器一起显示。
- `spinner_placement`：您可以指定旋转器元素的位置，默认为 'start'。

```python eval
docdemo(loading_states)
```

## 处理单击事件
您可以使用 `on_click` 事件参数来定义按钮被单击时发生的操作。例如，要在单击按钮时更改应用程序状态中的值：

```python demo box
eval(button_state2_render_code)
```

```python
{button_state2_code.strip()}
```

在上面的代码中，单击按钮后通过 `set_text_value` 事件处理程序更改 `text_value` 的值。Reflex 为每个基础变量提供了默认的 setter `event_handler`，可以通过在基础变量前加上 `set_` 关键字来访问。

以下是另一个示例，它创建了两个按钮来增加和减少计数值：

```python demo box
eval(button_state_example)
```

```python
{button_state_code.strip()}
```

在此示例中，我们有一个 `ButtonState` 状态类，它维护一个计数基础变量。当单击 "Increment" 按钮时，它会触发 `ButtonState.increment` 事件处理程序，当单击 "Decrement" 按钮时，它会触发 `ButtonState.decrement` 事件处理程序。

## 特殊事件和服务器端操作

在 Reflex 中，按钮可以触发特殊事件和服务器端操作，从而使您能够创建动态和交互式的用户体验。您可以使用 `on_click` 属性将这些事件绑定到按钮上。有关可用的特殊事件和服务器端操作的详细信息和用法示例，请参阅
[Special Events Documentation](/docs/api-reference/special-events)。

## 分组按钮
在 Reflex 应用程序中，您可以使用 `Stack` 组件和 `ButtonGroup` 组件有效地分组按钮。这些选项都提供了独特的功能，帮助您结构化和样式化您的按钮。

## 使用 `Stack` 组件
`Stack` 组件允许您垂直和水平堆叠按钮，为您的按钮排列提供了灵活的布局。

## 垂直堆叠按钮：

```python eval
docdemo(stack_buttons_vertical)
```

## 水平堆叠按钮：

```python eval
docdemo(stack_buttons_horizontal)
```
使用 `stack` 组件，您可以轻松创建垂直和水平按钮布局。

## 使用 `rx.button_group` 组件
`ButtonGroup` 组件专门用于按钮分组。它允许您：
- 设置其中所有按钮的 `size` 和 `variant`。
- 在按钮之间添加 `spacing`。
- 根据需要移除其子元素的边框半径，使按钮紧密排列。

```python eval
docdemo(button_group)
```

```md alert 
# The `ButtonGroup` component stacks buttons horizontally, whereas the `Stack` component allows stacking buttons both vertically and horizontally.
```

