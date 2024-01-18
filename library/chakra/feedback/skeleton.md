---
components:
    - rx.chakra.Skeleton
    - rx.chakra.SkeletonCircle
    - rx.chakra.SkeletonText
---

```python exec
import reflex as rx
```

# 骨架屏

骨架屏用于展示一些组件的加载状态。

```python demo
rx.stack(
    rx.skeleton(height="10px", speed=1.5),
    rx.skeleton(height="15px", speed=1.5),
    rx.skeleton(height="20px", speed=1.5),
    width="50%",
)
```

除了基本的骨架框外，还提供了骨架圆和文本，以方便使用。

```python demo
rx.stack(
    rx.skeleton_circle(size="30px"),
    rx.skeleton_text(no_of_lines=8),
    width="50%",
)
```

骨架屏的另一个特性是能够动画显示颜色。
我们提供了`start_color`和`end_color`参数来实现骨架组件的颜色动画效果。

```python demo
rx.stack(
    rx.skeleton_text(
        no_of_lines=5, start_color="pink.500", end_color="orange.500"
    ),
    width="50%",
)
```

您可以通过使用`is_loaded`属性来阻止骨架屏的加载。

```python demo
rx.vstack(
    rx.skeleton(rx.text("Text is already loaded."), is_loaded=True),
    rx.skeleton(rx.text("Text is already loaded."), is_loaded=False),
)
```

