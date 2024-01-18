将其翻译为中文：

---
components:
    - rx.chakra.Progress
---

```python exec
import reflex as rx
```

# 进度条

进度条用于显示长时间任务或由多个步骤组成的任务的进度状态。

```python demo
rx.vstack(
    rx.progress(value=0, width="100%"),
    rx.progress(value=50, width="100%"),
    rx.progress(value=75, width="100%"),
    rx.progress(value=100, width="100%"),
    rx.progress(is_indeterminate=True, width="100%"),
    spacing="1em",
    min_width=["10em", "20em"],
)
```

