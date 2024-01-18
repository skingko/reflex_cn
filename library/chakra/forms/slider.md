---
components:
    - rx.chakra.Slider
    - rx.chakra.SliderTrack
    - rx.chakra.SliderFilledTrack
    - rx.chakra.SliderThumb
    - rx.chakra.SliderMark
---

```python exec
import reflex as rx
```

# 滑动条

滑动条用于允许用户从一系列数值中进行选择。

```python demo exec
class SliderState(rx.State):
    value: int = 50


def slider_example():
    return rx.vstack(
        rx.heading(SliderState.value),
        rx.slider(
            on_change=SliderState.set_value
        ),
        width="100%",
    )
```

你也可以组合使用三个事件处理程序：`on_change`、`on_change_start`和`on_change_end`。

```python demo exec
class SliderCombo(rx.State):
    value: int = 50
    color: str = "black"

    def set_start(self, value):
        self.color = "#68D391" 

    def set_end(self, value):
        self.color = "#F56565" 


def slider_combo_example():
    return rx.vstack(
        rx.heading(SliderCombo.value, color=SliderCombo.color),
        rx.slider(
            on_change_start=SliderCombo.set_start,
            on_change=SliderCombo.set_value,
            on_change_end=SliderCombo.set_end,
        ),
        width="100%",
    )
```

你还可以通过传入自定义组件来自定义滑动条的外观。

```python demo exec
class SliderManual(rx.State):
    value: int = 50

    def set_end(self, value: int):
        self.value = value


def slider_manual_example():
    return rx.vstack( 
        rx.heading(f"Weather is {SliderManual.value} degrees"),
        rx.slider(
            rx.slider_track(
                rx.slider_filled_track(bg="tomato"),
                bg='red.100'
            ),
            rx.slider_thumb(
                rx.icon(tag="sun", color="white"),
                box_size="1.5em",
                bg="tomato",
            ),
            on_change_end=SliderManual.set_end,
        ),
        width="100%",
    )
```

如果你想在每次滑动条移动时触发状态改变，可以使用`on_change`事件处理程序。

出于性能考虑，当用户释放滑动条时才触发状态改变，你可以使用`on_change_end`事件处理程序，但如果你需要在每次滑动条移动时执行一个事件，可以使用`on_change`事件处理程序。

```python demo
rx.vstack(
    rx.heading(SliderState.value),
    rx.slider(
        on_change=SliderState.set_value
    ),
    width="100%",
)
```

