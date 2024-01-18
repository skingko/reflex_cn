---
components:
    - rx.radix.themes.Avatar
---
# 头像

```python exec
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
from pcweb.templates.docpage import style_grid
```

头像组件用于表示用户，并显示其个人资料图片或者回退文字（如初始字母）。

## 基本示例

要创建带有图像的头像组件，我们将图像的 URL 传递给 `src` prop。

```python demo
avatar(src="/logo.jpg")
```

如果我们只想显示文字（如初始字母），我们可以将其设置为 `fallback` prop，而无需传递 `src` prop。

```python demo
avatar(fallback="RX")
```

## 样式

```python eval
style_grid(component_used=avatar, component_used_str="avatar", variants=["solid", "soft"], fallback="RX")
```

### 大小

我们使用 size prop 来控制头像的尺寸。可接受的尺寸范围是从 "1" 到 "9"，其中 "3" 是默认值。

```python demo
flex(
    avatar(src="/logo.jpg", fallback="RX", size="1"),
    avatar(src="/logo.jpg", fallback="RX", size="2"),
    avatar(src="/logo.jpg", fallback="RX", size="3"),
    avatar(src="/logo.jpg", fallback="RX"),
    avatar(src="/logo.jpg", fallback="RX", size="4"),
    avatar(src="/logo.jpg", fallback="RX", size="5"),
    avatar(src="/logo.jpg", fallback="RX", size="6"),
    avatar(src="/logo.jpg", fallback="RX", size="7"),
    avatar(src="/logo.jpg", fallback="RX", size="8"),
    gap="1",
)
```

### 变体

我们使用 variant prop 来控制头像回退文字的视觉样式。variant prop 可以是 "solid" 或 "soft"。默认值为 "soft"。

```python demo
flex(
    avatar(fallback="RX", variant="solid"),
    avatar(fallback="RX", variant="soft"),
    avatar(fallback="RX"),
    gap="2",
)
```

### 颜色方案

我们使用 `color_scheme` prop 来为回退文字指定特定的颜色，忽略全局主题。

```python demo
flex(
    avatar(fallback="RX", color_scheme="indigo"),
    avatar(fallback="RX", color_scheme="cyan"),
    avatar(fallback="RX", color_scheme="orange"),
    avatar(fallback="RX", color_scheme="crimson"),
    gap="2",
)
```

### 高对比度

我们使用 `high_contrast` prop 来增加回退文字与背景之间的颜色对比度。

```python demo
grid(
    avatar(fallback="RX", variant="solid"),
    avatar(fallback="RX", variant="solid", high_contrast=True),
    avatar(fallback="RX", variant="soft"),
    avatar(fallback="RX", variant="soft", high_contrast=True),
    rows="2",
    gap="2",
    flow="column",
)
```

### 圆角

我们使用 `radius` prop 来指定特定的圆角值，忽略全局主题。它可以取值 "none" | "small" | "medium" | "large" | "full"。

```python demo
grid(
    avatar(src="/logo.jpg", fallback="RX", radius="none"),
    avatar(fallback="RX", radius="none"),
    avatar(src="/logo.jpg", fallback="RX", radius="small"),
    avatar(fallback="RX", radius="small"),
    avatar(src="/logo.jpg", fallback="RX", radius="medium"),
    avatar(fallback="RX", radius="medium"),
    avatar(src="/logo.jpg", fallback="RX", radius="large"),
    avatar(fallback="RX", radius="large"),
    avatar(src="/logo.jpg", fallback="RX", radius="full"),
    avatar(fallback="RX", radius="full"),
    rows="2",
    gap="2",
    flow="column",
)
```

### 回退文字

我们使用 `fallback` prop 来修改渲染的回退文字。

```python demo
flex(
    avatar(fallback="RX"),
    avatar(fallback="PC"),
    gap="2",
)
```

## 完整示例

在下面的示例中，我们使用 Avatar 组件构建用户个人资料页面的一部分。Avatar 组件用于显示用户的个人资料图片，回退文字为用户的初始字母。我们使用 Text 组件来显示用户的全名和用户名。我们使用 Button 组件来显示编辑个人资料按钮。

```python demo
flex(
    avatar(src="/logo.jpg", fallback="RU", size="9"),
    text("Reflex User", weight="bold", size="4"),
    text("@reflexuser", color_scheme="gray"),
    button("Edit Profile", color_scheme="indigo", variant="solid"),
    direction="column",
    gap="1",
)
```

