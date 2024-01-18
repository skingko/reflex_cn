---

components:
  - rx.radix.themes.Link

---

```python exec
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
```


# 链接

链接是可访问的元素，主要用于导航。使用 `href` 属性指定链接要导航到的位置。

```python demo
link("Reflex Home Page.", href="https://reflex.dev")
```

你也可以提供本地链接到项目中的其他页面，而不需要编写完整的 URL。

```python demo
link("Example", href="/docs/library",)
```

`link` 组件可用于包装其他组件，使它们链接到其他页面。

```python demo
link(button("Example"), href="https://reflex.dev")
```

您还可以使用 `id` 属性创建锚点，链接到页面的特定部分。

```python demo
box("Example", id="example")
```

要引用锚点，您可以使用 `link` 组件的 `href` 属性。`href` 应该是要链接到的页面的格式，后跟 # 和锚点的 id。

```python demo
link("Example", href="/docs/library/typography/link#example")
```


# 样式


## 大小

使用 `size` 属性控制链接的大小。该属性还提供正确的行高和矫正的字母间距 - 随着文本大小的增加，相对行高和字母间距减小。

```python demo
flex(
    link("The quick brown fox jumps over the lazy dog.", size="1"),
    link("The quick brown fox jumps over the lazy dog.", size="2"),
    link("The quick brown fox jumps over the lazy dog.", size="3"),
    link("The quick brown fox jumps over the lazy dog.", size="4"),
    link("The quick brown fox jumps over the lazy dog.", size="5"),
    link("The quick brown fox jumps over the lazy dog.", size="6"),
    link("The quick brown fox jumps over the lazy dog.", size="7"),
    link("The quick brown fox jumps over the lazy dog.", size="8"),
    link("The quick brown fox jumps over the lazy dog.", size="9"),
    direction="column",
    gap="3",
)
```

## 字重

使用 `weight` 属性设置文本的字重。

```python demo
flex(
    link("The quick brown fox jumps over the lazy dog.", weight="light"),
    link("The quick brown fox jumps over the lazy dog.", weight="regular"),
    link("The quick brown fox jumps over the lazy dog.", weight="medium"),
    link("The quick brown fox jumps over the lazy dog.", weight="bold"),
    direction="column",
    gap="3",
)
```

## 修剪

使用 `trim` 属性来修剪渲染文本的开头、结尾或两侧的空格。

```python demo
flex(
    link("Without Trim",
        trim="normal",
        style={"background": "var(--gray-a2)",
                "border_top": "1px dashed var(--gray-a7)",
                "border_bottom": "1px dashed var(--gray-a7)",}
    ),
    link("With Trim",
        trim="both",
        style={"background": "var(--gray-a2)",
                "border_top": "1px dashed var(--gray-a7)",
                "border_bottom": "1px dashed var(--gray-a7)",}
    ),
    direction="column",
    gap="3",
)
```

## 下划线

使用 `underline` 属性管理下划线指示的可见性。默认为 `auto`。

```python demo
flex(
    link("The quick brown fox jumps over the lazy dog.", underline="auto"),
    link("The quick brown fox jumps over the lazy dog.", underline="hover"),
    link("The quick brown fox jumps over the lazy dog.", underline="always"),
    direction="column",
    gap="3",
)
```

## 颜色

使用 `color_scheme` 属性分配指定的颜色，忽略全局主题。

```python demo
flex(
    link("The quick brown fox jumps over the lazy dog.", color_scheme="indigo"),
    link("The quick brown fox jumps over the lazy dog.", color_scheme="cyan"),
    link("The quick brown fox jumps over the lazy dog.", color_scheme="crimson"),
    link("The quick brown fox jumps over the lazy dog.", color_scheme="orange"),
    direction="column",
)
```

## 高对比度

使用 `high_contrast` 属性增加与背景的颜色对比度。

```python demo
flex(
    link("The quick brown fox jumps over the lazy dog."),
    link("The quick brown fox jumps over the lazy dog.", high_contrast=True),
    direction="column",
)
```

