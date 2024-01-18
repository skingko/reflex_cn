---
components:
    - rx.radix.themes.TextFieldRoot
    - rx.radix.themes.TextFieldInput
    - rx.radix.themes.TextFieldSlot
---

```python exec
import reflex as rx
import reflex.components.radix.themes as rdxt
```

# 文本框

文本框是用户可以输入文本的输入框。该组件使用了 Radix 的 [文本框](https://radix-ui.com/primitives/docs/components/text-field) 组件。

## 基本示例

```python demo
rdxt.textfield_root(
    rdxt.textfield_slot(
        rdxt.icon(tag="magnifying_glass"),
    ),
    rdxt.textfield_input(
        placeholder="Search here...",
    ),
)
```

```python demo exec
class TextfieldBlur(rx.State):
    text: str = "Hello World!"


def blur_example():
    return rx.vstack(
        rdxt.heading(TextfieldBlur.text),
        rdxt.textfield_root(
    rdxt.textfield_slot(
        rdxt.icon(tag="magnifying_glass"),
    ),
    rdxt.textfield_input(
        placeholder="Search here...",
        on_blur=TextfieldBlur.set_text,
    ),
    
)
    )
```


```python demo exec
class TextfieldControlled(rx.State):
    text: str = "Hello World!"


def controlled_example():
    return rx.vstack(
        rdxt.heading(TextfieldControlled.text),
        rdxt.textfield_root(
    rdxt.textfield_slot(
        rdxt.icon(tag="magnifying_glass"),
    ),
    rdxt.textfield_input(
        placeholder="Search here...",
        value=TextfieldControlled.text,
        on_change=TextfieldControlled.set_text,
    ),
    
)
    )
```


# 真实世界示例

```python demo exec

def song(title, initials: str, genre: str):
    return rdxt.card(rdxt.flex(
        rdxt.flex(
            rdxt.avatar(fallback=initials),
            rdxt.flex(
                rdxt.text(title, size="2", weight="bold"),
                rdxt.text(genre, size="1", color_scheme="gray"),
                direction="column",
                gap="1",
            ),
            direction="row",
            align_items="left",
            gap="1",
        ),
        rdxt.flex(
            rdxt.icon(tag="chevron_right"),
            align_items="center",
        ),
        justify="between",
    ))

def search():
    return rdxt.card(
    rdxt.flex(
        rdxt.textfield_root(
            rdxt.textfield_slot(
                rdxt.icon(tag="magnifying_glass"),
            ),
            rdxt.textfield_input(
                placeholder="Search songs...",
            ),
        ),
        rdxt.flex(
            song("The Less I Know", "T", "Rock"),
            song("Breathe Deeper", "ZB", "Rock"),
            song("Let It Happen", "TF", "Rock"),
            song("Borderline", "ZB", "Pop"),
            song("Lost In Yesterday", "TO", "Rock"),
            song("Is It True", "TO", "Rock"),
            direction="column",
            gap="1",
        ),
        direction="column",
        gap="3",
    ),
    style={"maxWidth": 500},
)
```

