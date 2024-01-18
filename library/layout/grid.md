---
components:
  - rx.radix.themes.Grid
---

```python exec
import reflex as rx
import reflex.components.radix.themes as rdxt
```

# 网格

用于创建网格布局的组件。可以指定`rows`或`columns`。

## 基本示例

```python demo
rdxt.grid(
    rx.foreach(
        rx.Var.range(12),
        lambda i: rdxt.card(f"Card {i + 1}", height="10vh"),
    ),
    columns="3",
    gap="4",
    width="100%",
)
```

```python demo
rdxt.grid(
    rx.foreach(
        rx.Var.range(12),
        lambda i: rdxt.card(f"Card {i + 1}", height="10vh"),
    ),
    rows="3",
    flow="column",
    justify="between",
    gap="4",
    width="100%",
)
```

