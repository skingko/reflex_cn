---
组件:
    - rx.chakra.Avatar
    - rx.chakra.AvatarBadge
    - rx.chakra.AvatarGroup
---

```python exec
import reflex as rx
```

# 头像

头像组件用于表示用户，并显示个人头像、姓名首字母或备用图标。

```python demo
rx.hstack(
    rx.avatar(size="sm"),
    rx.avatar(name="Barack Obama", size="md"),
    rx.avatar(name="Donald Trump", size="lg"),
    rx.avatar(name="Joe Biden", size="xl"),
)
```

头像组件可以分组展示，以便更容易显示。

```python demo
rx.avatar_group(
    rx.avatar(name="Barack Obama"),
    rx.avatar(name="Donald Trump"),
    rx.avatar(name="Joe Biden"),
)
```

徽章也可以用来显示头像的状态，例如活动状态。

```python demo
rx.avatar_group(
    rx.avatar(
        rx.avatar_badge(
            box_size="1.25em", bg="green.500", border_color="green.500"
        ),
        name="Barack Obama",
    ),
    rx.avatar(
        rx.avatar_badge(
            box_size="1.25em", bg="yellow.500", border_color="red.500"
        ),
        name="Donald Trump",
    ),
)
```

如果有太多的头像需要展示，可以使用`max_`属性设置上限。

```python demo
rx.avatar_group(
    *([rx.avatar(name="Barack Obama")] * 5),
    size="md",
    max_=3,
)
```

