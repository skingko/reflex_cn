---
components:
  - rx.radix.themes.Container
---

```python exec
import reflex.components.radix.themes as rdxt
```

# 容器

用于限制页面内容的最大宽度，同时保持灵活的边距以实现响应式布局。

通常使用容器来包裹页面的主要内容。

## 基本示例

```python demo
rdxt.box(
    rdxt.container(
        rdxt.card("This content is constrained to a max width of 448px.", width="100%"),
        size="1",
    ),
    rdxt.container(
        rdxt.card("This content is constrained to a max width of 688px.", width="100%"),
        size="2",
    ),
    rdxt.container(
        rdxt.card("This content is constrained to a max width of 880px.", width="100%"),
        size="3",
    ),
    rdxt.container(
        rdxt.card("This content is constrained to a max width of 1136px.", width="100%"),
        size="4",
    ),
    background_color="var(--gray-3)",
    width="100%",
)
```

