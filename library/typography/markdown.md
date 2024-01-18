---

components:
    - rx.Markdown
---

```python exec
import reflex as rx
```

# Markdown

`rx.markdown` 组件可以用来渲染 Markdown 文本。
它基于 [Github Flavored Markdown](https://github.github.com/gfm/)。

```python demo
rx.vstack(
    rx.markdown("# Hello World!"),
    rx.markdown("## Hello World!"),
    rx.markdown("### Hello World!"),
    rx.markdown("Support us on [Github](https://github.com/reflex-dev/reflex)."),
    rx.markdown("Use `reflex deploy` to deploy your app with **a single command**."),
)
```

## 数学公式

你可以使用 LaTeX 渲染数学公式。
对于行内公式，可以使用 `$` 包围公式：

```python demo
rx.markdown("Pythagorean theorem: $a^2 + b^2 = c^2$.")
```

## 语法高亮

使用 \`\`\`\{language} 语法可以渲染带有语法高亮的代码块：

```python demo  
rx.markdown(
r"""
\```python
import reflex as rx
from .pages import index

app = rx.App()
app.add_page(index)
\```
"""
)
```

## 表格

使用 `|` 语法可以渲染表格：

```python demo
rx.markdown(
    """
| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |
"""
)
```

## 组件映射

你可以使用 `component_map` 属性来指定渲染 Markdown 元素时使用的组件。

`component_map` 属性中的每个键都代表一个 Markdown 元素，值则是一个以元素文本为输入的函数，返回一个 Reflex 组件。

```md alert
The `codeblock` and `a` tags are special cases. In addition to the `text`, they also receive a `props` argument containing additional props for the component.
```

```python demo exec
component_map = {
    "h1": lambda text: rx.heading(text, size="lg", margin_y="1em"),
    "h2": lambda text: rx.heading(text, size="md", margin_y="1em"),
    "h3": lambda text: rx.heading(text, size="sm", margin_y="1em"),
    "p": lambda text: rx.text(text, color="green", margin_y="1em"),
    "code": lambda text: rx.code(text, color="purple"),
    "codeblock": lambda text, **props: rx.code_block(text, **props, theme="dark", margin_y="1em"),
    "a": lambda text, **props: rx.link(text, **props, color="blue", _hover={"color": "red"}),
}

def index():
    return rx.box(
        rx.markdown(
r"""
# Hello World!

## This is a Subheader

### And Another Subheader

Here is some `code`:

\```python
import reflex as rx

component = rx.text("Hello World!")
\```

And then some more text here, followed by a link to [Reflex](https://reflex.dev).
""",
    component_map=component_map,
)
    )
```

