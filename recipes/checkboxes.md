```python exec
import reflex as rx
```

# 智能复选框组

一个智能复选框组，您可以跟踪所有选中的框，并设置选中框的数量限制。

## 步骤

```python eval
rx.center(rx.image(src="/gallery/smart_checkboxes.gif")),
```

此步骤使用一个 `dict[str, bool]` 来跟踪复选框的状态。
此外，使用一个计算变量限制用户选中的框的数量。

```python
class CBoxeState(rx.State):
    
    choices: dict[str, bool] = \{k: False for k in ["Choice A", "Choice B", "Choice C"]}
    _check_limit = 2

    def check_choice(self, value, index):
        self.choices[index] = value

    @rx.var
    def choice_limit(self):
        return sum(self.choices.values()) >= self._check_limit

    @rx.var
    def checked_choices(self):
        choices = [l for l, v in self.choices.items() if v]
        return " / ".join(choices) if choices else "None"

import reflex as rx


def render_checkboxes(values, limit, handler):
    return rx.vstack(
        rx.checkbox_group(
            rx.foreach(
                values,
                lambda choice: rx.checkbox(
                    choice[0],
                    is_checked=choice[1],
                    is_disabled=~choice[1] & limit,
                    on_change=lambda val: handler(val, choice[0]),
                ),
            )
        )
    )


def index() -> rx.Component:
    
    return rx.center(
        rx.vstack(
            rx.text("Make your choices (2 max):"),
            render_checkboxes(
                CBoxeState.choices,
                CBoxeState.choice_limit,
                CBoxeState.check_choice,
            ),
            rx.text("Your choices: ", CBoxeState.checked_choices),
        ),
        height="100vh",
    )
```

