---
components:
    - rx.radix.themes.Checkbox
---

```python exec
import reflex as rx
import reflex.components.radix.themes as rdxt
```


# 复选框

复选框允许用户从一组中选择一个或多个项目。该组件使用 Radix 的 [checkbox](https://radix-ui.com/primitives/docs/components/checkbox) 组件。

## 基本示例

```python demo
rdxt.text(
  rdxt.flex(
    rdxt.checkbox(default_checked=True),
    "Agree to Terms and Conditions", 
    gap="2",
  ),
  as_="label",
  size="2",
)
```

## 属性

### Disabled

`disabled` 属性用于禁用按钮，默认值为 `False`。禁用的按钮不会响应用户的交互操作，如点击，也不能获得焦点。

```python demo
rx.hstack(
    rdxt.checkbox(),
    rdxt.checkbox(disabled=True),
)
```

## 触发器

### OnCheckedChange

`on_change` 触发器在复选框被点击时被调用。
```python demo
rdxt.checkbox(default_checked=True, on_checked_change=rx.window_alert("Checked!"))
```


## 真实世界示例


```python demo
rdxt.flex(
   rdxt.heading("Terms and Conditions"),
   rdxt.text("Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed neque elit, tristique placerat feugiat ac, facilisis vitae arcu. Proin eget egestas augue. Praesent ut sem nec arcu 'pellentesque aliquet. Duis dapibus diam vel metus tempus vulputate.",
   ),
   rdxt.text(
      rdxt.flex(
        rdxt.checkbox(default_checked=True, color_scheme="indigo"),
        "I certify that I have read and agree to the terms and conditions for this reservation.", 
        gap="2",
      ),
      as_="label",
      size="2",
    ),
    rdxt.button("Book Reservation", color_scheme="indigo", width="100%"),
    direction="column",
    align_items="start",
    border="1px solid #e2e8f0",
    background_color="#f7fafc",
    border_radius="15px",
    gap="3",
    p="3",
)
```

