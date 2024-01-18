```python exec
import reflex as rx

from pcweb.pages.docs import api_reference
```

# 特殊事件

Reflex还内置了一些特殊事件，可以在[参考文档]({api_reference.special_events.path})中找到。

例如，一个事件处理程序可以在浏览器上触发一个警报。

```python demo exec
class SpecialEventsState(rx.State):
    def alert(self):
        return rx.window_alert("Hello World!")

def special_events_example():
    return rx.button("Alert", on_click=SpecialEventsState.alert)
```

