--- 
components:
    - rx.chakra.CircularProgress
    - rx.chakra.CircularProgressLabel
---

```python exec
import reflex as rx
```

# CircularProgress

CircularProgress 组件用于指示确定性和不确定性进程的进度。
确定性进度：随着指示器从0到360度的移动，填充圆形轨道的颜色。
不确定性进度：在沿圆形轨道移动时，指示器会增长和缩小。

```python demo
rx.hstack(
    rx.circular_progress(value=0),
    rx.circular_progress(value=25),
    rx.circular_progress(rx.circular_progress_label(50), value=50),
    rx.circular_progress(value=75),
    rx.circular_progress(value=100),
    rx.circular_progress(is_indeterminate=True),
)
```

