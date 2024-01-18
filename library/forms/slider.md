---

components:
    - rx.radix.themes.Slider
---

```python exec
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
from pcweb.templates.docpage import style_grid
```


# 滑块

提供用户从一系列的值中选择。

## 基本示例

```python demo
slider(default_value=[40], width="100%")
```


### 设置滑块默认值

我们可以为滑块的范围设置`min`和`max`的值。默认的`min`和`max`值为0和100。

还可以使用`step`属性调整步进间隔。默认为1。

当值在交互结束时发生变化时，会触发`on_value_commit`事件。当你只需要获取最终值时，比如更新后端服务时，这个事件很有用。

```python demo exec
class SliderVariationState(rx.State):
    value: int = 50

    def set_end(self, value: int):
        self.value = value

def slider_max_min_step():
    return rx.vstack(
        heading(SliderVariationState.value),
        text("Min=20 Max=240"),
        slider(default_value=[40], min=20, max=240, width="100%", on_value_commit=SliderVariationState.set_end),
        text("Step=5"),
        slider(default_value=[40], step=5, width="100%", on_value_commit=SliderVariationState.set_end),
        text("Step=0.5"),
        slider(default_value=[40], step=0.5, width="100%", on_value_commit=SliderVariationState.set_end),
        width="100%",
    )
```


### 禁用

当将`disabled`属性设置为`True`时，它会阻止用户与滑块进行交互。

```python demo
slider(default_value=[40], width="100%", disabled=True)
```


### 控制数值

`default_value`是滑块在初始渲染时的值。它必须作为`List[float]`传递。你可以传入多个`float`值，这样可以渲染多个可拖动的滑块。提供多个值可以创建一个范围滑块。


```python demo
slider(default_value=[40, 60], width="100%")
```


当滑块的`value`改变时，会触发`on_value_change`事件。


```python demo exec
class SliderVariationState2(rx.State):
    value: int = 50

    def set_end(self, value: int):
        self.value = value


def slider_on_value_change():
    return rx.vstack(
        heading(SliderVariationState2.value),
        slider(default_value=[40], width="100%", on_value_change=SliderVariationState2.set_end),
        width="100%",
    )
```




### 使用滑块提交表单

滑块的`name`属性。作为名称/值对的一部分提交到所属表单。


```python demo exec
class FormSliderState(rx.State):
    form_data: dict = {}

    def handle_submit(self, form_data: dict):
        """Handle the form submit."""
        self.form_data = form_data


def form_example2():
    return rx.vstack(
        rx.form(
            rx.vstack(
                slider(default_value=[40], width="100%", name="slider"),
                rx.button("Submit", type_="submit"),
                width="100%",
            ),
            on_submit=FormSliderState.handle_submit,
            reset_on_submit=True,
            width="100%",
        ),
        rx.divider(),
        rx.heading("Results"),
        rx.text(FormSliderState.form_data.to_string()),
        width="100%",
    )
```



### 方向

使用`orientation`属性来改变滑块的方向。

```python demo
slider(default_value=[40], width="100%", orientation="horizontal")
```

```python demo
slider(default_value=[40], height="4em", orientation="vertical")
```






## 样式

```python eval
style_grid(component_used=slider, component_used_str="slider", variants=["classic", "surface", "soft"], disabled=True, default_value=[40], width="100%",)
```

### 大小

```python demo
flex(
    slider(default_value=[25], size="1"),
    slider(default_value=[25], size="2"),
    slider(default_value=[25], size="3"),
    direction="column",
    gap="4",
    width="100%",
)
```



### 高对比度

```python demo
flex(
    slider(default_value=[25]),
    slider(default_value=[25], high_contrast=True),
    direction="column",
    gap="4",
    width="100%",
)
```


### 圆角

```python demo
flex(
    slider(default_value=[25], radius="none"),
    slider(default_value=[25], radius="small"),
    slider(default_value=[25], radius="medium"),
    slider(default_value=[25], radius="large"),
    slider(default_value=[25], radius="full"),
    direction="column",
    gap="4",
    width="100%",
)
```



## 真实世界示例




