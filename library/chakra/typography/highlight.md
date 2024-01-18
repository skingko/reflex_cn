---
components:
    - rx.chakra.Highlight
---

```python exec
import reflex as rx
```

# 高亮显示

高亮显示组件接受一个字符串作为输入，并将其中的一些单词以高亮文本的形式显示出来。

可以使用 `query` 属性来选择要高亮显示的单词。

还可以通过 `styles` 属性自定义高亮显示的样式。

```python demo
rx.highlight("Hello World, we have some highlight", query=['World','some'], styles={ 'px': '2', 'py': '1', 'rounded': 'full', 'bg': 'grey' })
```

