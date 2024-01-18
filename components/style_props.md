```python exec
from pcweb.pages.docs import styling
import reflex as rx
```

# 样式属性

除了组件特定的属性之外，大多数内置组件都支持完整的样式属性。您可以使用任何 CSS 属性来为组件设置样式。

```python demo
rx.button(
    "Fancy Button",
    border_radius="1em",
    box_shadow="rgba(151, 65, 252, 0.8) 0 15px 30px -10px",
    background_image="linear-gradient(144deg,#AF40FF,#5B42F3 50%,#00DDEB)",
    box_sizing="border-box",
    color="white",
    opacity="0.6",
    _hover={
        "opacity": 1,
    }
)
```

请参阅 [样式文档]({styling.overview.path}) 以了解有关自定义应用外观的更多信息。

