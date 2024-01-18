```python exec
import reflex as rx
from pcweb.pages.docs import styling
```

# 样式

可以使用完整的 [CSS](https://www.w3schools.com/css/) 对 Reflex 组件进行样式设置。

以下是添加样式到应用程序的三种主要方式，按照以下顺序优先级递减：
1. **内联样式（Inline）**：应用于单个组件实例的样式。
2. **组件样式（Component）**：应用于特定类型的组件的样式。
3. **全局样式（Global）**：应用于所有组件的样式。

```md alert success
# Style keys can be any valid CSS property name.
To be consistent with Python standards, you can specify keys in `snake_case`.
```

## 全局样式

您可以将样式字典传递给应用程序，以应用基础样式到所有组件。

例如，您可以在此处设置应用程序的默认字体和字体大小，而无需在每个组件上设置。

```python
style = {
    "font_family": "Comic Sans MS",
    "font_size": "16px",
}

app = rx.App(style=style)
```

## 组件样式

在样式字典中，您还可以为特定组件类型或自定义的 CSS 类和 ID 指定默认样式。

```python
accent_color = "#f81ce5"
style = {
    "::selection": {
        "background_color": accent_color,
    },
    ".some-css-class": {
        "text_decoration": "underline",
    },
    "#special-input": \{"width": "20vw"},
    rx.Text: {
        "font_family": styles.SANS,
    },
    rx.Divider: {
        "margin_bottom": "1em",
        "margin_top": "0.5em",
    },
    rx.Heading: {
        "font_weight": "500",
    },
    rx.Code: {
        "color": accent_color,
    },
}

app = rx.App(style=style)
```

使用此类样式字典，您可以轻松创建应用程序的一致主题。

```md alert
# Note the use of the uppercase component names.
We specify the component classes as keys, rather than their constructors.
```

```md alert warning
# Watch out for underscores in class names and IDs
Reflex automatically converts `snake_case` identifiers into `camelCase` format when applying styles. To ensure consistency, it is recommended to use the dash character or camelCase identifiers in your own class names and IDs. To style third-party libraries relying on underscore class names, an external stylesheet should be used. See [custom stylesheets]({styling.custom_stylesheets.path}) for how to reference external CSS files.
```

## 内联样式

内联样式适用于单个组件实例。它们以普通的 props 形式传递给组件。

```python demo
rx.text(
    "Hello World",
    background_image="linear-gradient(271.68deg, #EE756A 0.75%, #756AEE 88.52%)",
    background_clip="text",
    font_weight="bold",
    font_size="2em",
)
```

子组件会继承内联样式，除非被自身的内联样式覆盖。

```python demo
rx.box(
    rx.hstack(
        rx.button("Default Button"),
        rx.button("Red Button", color="red"),
    ),
    color="blue",
)
```

## Tailwind

Reflex 支持开箱即用的 [Tailwind CSS](https://tailwindcss.com/)。要启用它，请在 `rxconfig.py` 的 `tailwind` 参数中传递一个字典：

```python
import reflex as rx


class AppConfig(rx.Config):
    pass


config = AppConfig(
    app_name="app",
    db_url="sqlite:///reflex.db",
    env=rx.Env.DEV,
    tailwind=\{},
)
```

支持所有的 Tailwind 配置选项。插件和预设会自动包装 `require()`：

```python
config = AppConfig(
    app_name="app",
    db_url="sqlite:///reflex.db",
    env=rx.Env.DEV,
    tailwind={
        "theme": {
            "extend": \{},
        },
        "plugins": ["@tailwindcss/typography"],
    },
)
```

您可以在 `class_name` 属性下使用任何 [实用工具类](https://tailwindcss.com/docs/utility-first)：

```python demo
rx.box(
    "Hello World",
    class_name="text-4xl text-center text-blue-500",
)
```

## 禁用 Tailwind

如果要在配置中禁用 Tailwind，请将 `tailwind` 配置设置为 `None`。这在需要临时关闭项目的 Tailwind 时非常有用：

```python
config = rx.Config(app_name="app", tailwind=None)
```

使用此配置，Tailwind 将被禁用，不会将任何 Tailwind 样式应用于您的应用程序。


## 特殊样式

我们支持 Chakra UI 的所有 [伪类样式](https://chakra-ui.com/docs/features/style-props#pseudo)。

以下是一个在悬停时更改颜色的文本示例。

```python demo
rx.box(
    rx.text("Hover Me", _hover={"color": "red"}),
)
```


## 样式属性

内联样式也可以使用 `style` 属性设置。这对于在多个组件之间重用样式非常有用。

```python exec
text_style = {
    "color": "green",
    "font_family": "Comic Sans MS",
    "font_size": "1.2em",
    "font_weight": "bold",
    "box_shadow": "rgba(240, 46, 170, 0.4) 5px 5px, rgba(240, 46, 170, 0.3) 10px 10px",
}
```

```python
text_style={text_style}
```

```python demo
rx.vstack(
    rx.text("Hello", style=text_style),
    rx.text("World", style=text_style),
)
```

```python exec
style1 = {
    "color": "green",
    "font_family": "Comic Sans MS",
    "border_radius": "10px",
    "background_color": "rgb(107,99,246)",
}
style2 = {
    "color": "white",
    "border": "5px solid #EE756A",
    "padding": "10px",
}
```

```python
style1={style1}
style2={style2}
```

```python demo
rx.box(
    "Multiple Styles",
    style=[style1, style2],
)
```

样式字典按照传入的顺序应用。这意味着后面定义的样式将覆盖先前定义的样式。

