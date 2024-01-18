```python exec
import reflex as rx
from pcweb.pages.docs import assets
```

# 自定义样式表

Reflex 允许你添加自定义样式表。只需将样式表的 URL 传递给 `rx.App`：

```python
app = rx.App(
    stylesheets=[
        "https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css",
    ],
)
```

## 本地样式表

你也可以添加本地样式表。只需将样式表放在 [`assets/`]({assets.upload_and_download_files.path}) 目录下，并将路径传递给 `rx.App`：

```python
app = rx.App(
    stylesheets=[
        "styles.css",  # This path is relative to assets/
    ],
)
```

## 字体

你可以利用 Reflex 对自定义样式表的支持，将自定义字体添加到你的应用中。

然后，通过设置 `font_family` 属性来在应用中使用该字体。

在本例中，我们将使用来自 Google Fonts 的 [IBM Plex Mono]({"https://fonts.google.com/specimen/IBM+Plex+Mono"}) 字体。

```python demo
rx.text(
    "Check out my font",
    font_family="IBM Plex Mono",
    font_size="1.5em",
)
```

## 本地字体

通过利用前两点，我们还可以创建一个样式表，让你可以使用托管在服务器上的字体。

如果你的字体名为 `MyFont.otf`，请将它复制到 `assets/fonts` 目录下。

现在，我们已经准备好字体了，让我们创建样式表 `myfont.css`。

```css
@font-face {
    font-family: MyFont;
    src: url("MyFont.otf") format("opentype");
}

@font-face {
    font-family: MyFont;
    font-weight: bold;
    src: url("MyFont.otf") format("opentype");
}
```

在你的应用中添加对新样式表的引用。

```python
app = rx.App(
    stylesheets=[
        "fonts/myfont.css",  # This path is relative to assets/
    ],
)
```

就这样！现在你可以像其他字体一样使用 `MyFont` 来为你的组件设置样式。

