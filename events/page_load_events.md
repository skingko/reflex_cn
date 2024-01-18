```python exec
import reflex as rx
```


# 页面加载事件
您还可以指定在页面加载时运行的函数。这对于在每次渲染或状态更改时只获取一次数据非常有用。
在这个示例中，我们在页面加载时获取数据:

```python
class State(rx.State):
    data: Dict[str, Any]

    def get_data(self):
        # Fetch data
        self.data = fetch_data()

@rx.page(on_load=State.get_data)
def index():
    return rx.text('A Beautiful App')
```

