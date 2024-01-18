```python exec
import reflex as rx
```
# 响应式

Reflex 应用程序可以根据移动设备、平板和桌面显示器进行响应式的展示，以保证良好的外观。

您可以将值列表传递给任何样式属性，以在不同的屏幕尺寸上指定其值。

```python demo
rx.text(
    "Hello World",
    color=["orange", "red", "purple", "blue", "green"],
)
```

文本的颜色将根据您的屏幕尺寸而改变。如果您使用的是桌面电脑，请尝试调整浏览器窗口的大小以查看颜色的变化。

默认的断点如下所示。

```json
"sm": '30em',
"md": '48em',
"lg": '62em',
"xl": '80em',
"2xl": '96em',
```

## 基于显示的组件展示

响应式的常见用例是根据屏幕尺寸显示不同的组件。

Reflex 提供了用于此目的的有用的辅助组件。

```python demo
rx.vstack(
    rx.desktop_only(
        rx.text("Desktop View"),
    ),
    rx.tablet_only(
        rx.text("Tablet View"),
    ),
    rx.mobile_only(
        rx.text("Mobile View"),
    ),
    rx.mobile_and_tablet(
        rx.text("Visible on Mobile and Tablet"),
    ),
    rx.tablet_and_desktop(
        rx.text("Visible on Desktop and Tablet"),
    ),
)
```

## 指定显示断点

您可以使用 `display` 样式属性来指定用于响应式组件的断点。

```python demo
rx.vstack(
    rx.text(
        "Hello World",
        color="green",
        display=["none", "none", "none", "none", "flex"],
    ),
    rx.text(
        "Hello World",
        color="blue",
        display=["none", "none", "none", "flex", "flex"],
    ),
    rx.text(
        "Hello World",
        color="red",
        display=["none", "none", "flex", "flex", "flex"],
    ),
    rx.text(
        "Hello World",
        color="orange",
        display=["none", "flex", "flex", "flex", "flex"],
    ),
    rx.text(
        "Hello World",
        color="yellow",
        display=["flex", "flex", "flex", "flex", "flex"],
    ),
)
```

