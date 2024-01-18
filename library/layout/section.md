---
components:
  - rx.radix.themes.Section
---

```python exec
import reflex.components.radix.themes as rdxt
```

# 区块

默认情况下，表示页面内容的一部分，并提供垂直内边距。

主要用作语义组件，用于分组相关的文本内容。

## 基本示例

```python demo
rdxt.box(
    rdxt.section(
        rdxt.heading("First"),
        rdxt.text("This is the first content section"),
        px="3",
        background_color="var(--gray-2)",
    ),
    rdxt.section(
        rdxt.heading("Second"),
        rdxt.text("This is the second content section"),
        px="2",
        background_color="var(--gray-2)",
    ),
    width="100%",
)
```

