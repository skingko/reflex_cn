---
components:
    - rx.chakra.Link
---

```python exec
import reflex as rx
```

# 链接

链接是主要用于导航的可访问元素。

```python demo
rx.link("Example", href="https://reflex.dev", color="rgb(107,99,246)")
```

您也可以在项目中为其他页面提供本地链接，而无需编写完整的 URL。

```python demo
rx.link("Example", href="/docs/library", color="rgb(107,99,246)")
```

链接组件可以用于包装其他组件，使它们链接到其他页面。

```python demo
rx.link(rx.button("Example"), href="https://reflex.dev", color="rgb(107,99,246)", button=True)
```

您还可以使用 id 属性创建锚点链接到页面的特定部分。

```python demo
rx.box("Example", id="example")
```

要引用锚点，您可以使用链接组件的 href 属性。
`href` 应该是要链接到的页面的格式，后面跟上 `#` 和锚点的 `id`。

```python demo
rx.link("Example", href="/docs/library/navigation/link#example", color="rgb(107,99,246)")
```

