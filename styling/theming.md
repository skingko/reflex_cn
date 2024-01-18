```python exec
import reflex as rx
```

# 主题

你还可以通过添加`rx.toggle_color_mode`到一个事件触发器来添加一个暗色模式切换。这将把整个应用程序切换到暗色模式。

这是一个将应用程序切换到暗色模式的按钮示例：

```python
rx.button(
    rx.icon(tag="moon"),
    on_click=rx.toggle_color_mode,
)
```

```md alert warning
# Any custom colors you add will not be overwritten by the dark mode toggle.
```

```python eval
rx.box(height=4)
```

更多主题选项即将推出！

