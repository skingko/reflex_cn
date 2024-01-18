# 侧边栏

类似导航栏，侧边栏是网页或应用程序中常见的界面元素之一。

## 配方

在本示例中，我们将创建一个侧边栏组件，可以帮助在Web应用中进行导航。

在此示例中，我们希望侧边栏固定在页面的左侧，因此我们将使用 `position="fixed"` 属性使侧边栏固定在页面的左侧。
我们还将使用 `left=0` 和 `z_index=1` 属性，以确保侧边栏始终位于屏幕顶部，并在页面上的其他组件之上。

```python
 import reflex as rx

def sidebar():
    return rx.box(
        rx.vstack(
            rx.image(src="/favicon.ico", margin="0 auto"),
            rx.heading("Sidebar", text_align="center", margin_bottom="1em"),
            rx.menu(...),
            width="250px",
            padding_x="2em",
            padding_y="1em",
        ),
        position="fixed",
        height="100%",
        left="0px",
        top="0px",
        z_index="500",
    )
```

