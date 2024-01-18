```python exec
import random
import time

import reflex as rx
```
＃ 计算变量

计算变量的值是根据后端上的其他属性导出的。它们在您的 State 类中被定义为使用`@rx.var`装饰器的方法。当事件与状态进行处理时，计算变量将被重新计算。

尝试在输入框中输入并点击空白处。

```python demo exec
class UppercaseState(rx.State):
    text: str = "hello"

    @rx.var
    def upper_text(self) -> str:
        # This will be recomputed whenever `text` changes.
        return self.text.upper()


def uppercase_example():
    return rx.vstack(
        rx.heading(UppercaseState.upper_text),
        rx.input(on_blur=UppercaseState.set_text, placeholder="Type here..."),
    )
```

这里，“upper_text”是一个计算变量，它始终保存`text`的大写版本。

我们建议始终为计算变量使用类型注解。



## 缓存变量

被装饰为`@rx.cached_var`的缓存变量是一种特殊类型的计算变量，仅当依赖的其他状态变量发生更改时才会重新计算。这对于代价高昂的计算很有用，但在某些情况下，它可能不会在您预期的时候更新。

```python demo exec
class CachedVarState(rx.State):
    counter_a: int = 0
    counter_b: int = 0

    @rx.var
    def last_touch_time(self) -> str:
        # This is updated anytime the state is updated.
        return time.strftime("%H:%M:%S")

    def increment_a(self):
        self.counter_a += 1

    @rx.cached_var
    def last_counter_a_update(self) -> str:
        # This is updated only when `counter_a` changes.
        return f"{self.counter_a} at {time.strftime('%H:%M:%S')}"

    def increment_b(self):
        self.counter_b += 1

    @rx.cached_var
    def last_counter_b_update(self) -> str:
        # This is updated only when `counter_b` changes.
        return f"{self.counter_b} at {time.strftime('%H:%M:%S')}"


def cached_var_example():
    return rx.vstack(
        rx.text(f"State touched at: {CachedVarState.last_touch_time}"),
        rx.text(f"Counter A: {CachedVarState.last_counter_a_update}"),
        rx.text(f"Counter B: {CachedVarState.last_counter_b_update}"),
        rx.hstack(
            rx.button("Increment A", on_click=CachedVarState.increment_a),
            rx.button("Increment B", on_click=CachedVarState.increment_b),
        ),
    )
```

在这个例子中，`last_touch_time`是一个普通的计算变量，它在状态被修改时更新。`last_counter_a_update`是一个只依赖于`counter_a`的计算变量，因此只有在`counter_a`发生变化时才会重新计算。类似地，`last_counter_b_update`只依赖于`counter_b`，因此只有在`counter_b`发生变化时才会更新。

