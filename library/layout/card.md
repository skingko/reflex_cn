---
components:
  - rx.radix.themes.Card
---

```python exec
import reflex as rx
import reflex.components.radix.themes as rdxt
```

# 卡片（Card）

卡片组件用于将相关组件分组。它类似于 Box，但卡片有边框，使用主题颜色和边框半径，并提供一个 `size` 属性来控制根据 Radix 的“1”-“5”刻度的间距和边距。

与主题一起使用时，相较于 Box，卡片需要较少的样式处理才能获得一致的视觉效果。

## 基本示例

```python demo
rdxt.flex(
    rdxt.card("Card 1", size="1"),
    rdxt.card("Card 2", size="2"),
    rdxt.card("Card 3", size="3"),
    rdxt.card("Card 4", size="4"),
    rdxt.card("Card 5", size="5"),
    gap="2",
    align_items="flex-start",
    flex_wrap="wrap",
)
```

## 作为不同元素进行渲染

可以使用 `as_child` 属性将卡片渲染为不同的元素。常用的是将卡片作为链接或按钮可点击。

```python demo
rdxt.card(
    rdxt.link(
        rdxt.flex(
            rdxt.avatar(src="/reflex_banner.png"),
            rdxt.box(
                rdxt.heading("Quick Start"),
                rdxt.text("Get started with Reflex in 5 minutes."),
            ),
            gap="2",
        ),
    ),
    as_child=True,
)
```

## 使用插入内容

```jsx
<Card>
  <Card.Inset>
    {/* 插入内容 */}
  </Card.Inset>
</Card>
```

插入内容可以用于在卡片内添加附加的元素，例如图标、标签或其他组件。

