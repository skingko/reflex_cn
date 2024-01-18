---

components:
    - rx.chakra.Grid（栅格）
    - rx.chakra.GridItem（栅格项）

---

```python exec
import reflex as rx
```

一个在网格布局中非常有用的基本组件。Grid（栅格）是一个具有display、grid属性并且带有有用的样式缩写的Box（盒子）组件。它渲染一个div元素。

```python demo
rx.grid(
    rx.grid_item(row_span=1, col_span=1, bg="lightgreen"),
    rx.grid_item(row_span=1, col_span=1, bg="lightblue"),
    rx.grid_item(row_span=1, col_span=1, bg="purple"),
    rx.grid_item(row_span=1, col_span=1, bg="orange"),
    rx.grid_item(row_span=1, col_span=1, bg="yellow"),
    template_columns="repeat(5, 1fr)",
    h="10em",
    width="100%",
    gap=4,
)
```

在某些布局中，你可能需要某些栅格项跨越特定的列数或行数，而不是均匀分布。为了实现这个目的，你需要将col_span属性传递给GridItem（栅格项）组件以跨越列，并且还需要传递row_span属性以跨越行。你还需要指定template_columns和template_rows。

```python demo
rx.grid(
    rx.grid_item(row_span=2, col_span=1, bg="lightblue"),
    rx.grid_item(col_span=2, bg="lightgreen"),
    rx.grid_item(col_span=2, bg="yellow"),
    rx.grid_item(col_span=4, bg="orange"),
    template_rows="repeat(2, 1fr)",
    template_columns="repeat(5, 1fr)",
    h="200px",
    width="100%",
    gap=4,
)
```

