# 徽章

```python exec
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
from pcweb.templates.docpage import style_grid
```

徽章用于突出显示项目的状态，以便快速识别。

## 基本示例

要创建一个只包含文本的徽章组件，我们将文本作为参数传递。

```python demo
badge("New")
```

## 样式

```python eval
style_grid(component_used=badge, component_used_str="badge", variants=["solid", "soft", "surface", "outline"], components_passed="England!",)
```

### 尺寸

我们使用 `size` 属性来改变徽章的尺寸。它可以取值为 `"1" | "2"`，默认值为 `"1"`。

```python demo
flex(
    badge("New"),
    badge("New", size="1"),
    badge("New", size="2"),
    align="center",
    gap="2",
)
```

### 变体

我们使用 `variant` 属性来控制视觉样式。支持的变体类型有 `"solid" | "soft" | "surface" | "outline"`。默认的变体是 `"soft"`。

```python demo
flex(
    badge("New", variant="solid"),
    badge("New", variant="soft"),
    badge("New"),
    badge("New", variant="surface"),
    badge("New", variant="outline"),
    gap="2",
)
```

### 颜色方案

我们使用 `color_scheme` 属性来分配特定的颜色，忽略全局主题。

```python demo
flex(
    badge("New", color_scheme="indigo"),
    badge("New", color_scheme="cyan"),
    badge("New", color_scheme="orange"),
    badge("New", color_scheme="crimson"),
    gap="2",
)
```

### 高对比度

我们使用 `high_contrast` 属性来增加与背景的颜色对比度。

```python demo
flex(
    flex(
        badge("New", variant="solid"),
        badge("New", variant="soft"),
        badge("New", variant="surface"),
        badge("New", variant="outline"),
        gap="2",
    ),
    flex(
        badge("New", variant="solid", high_contrast=True),
        badge("New", variant="soft", high_contrast=True),
        badge("New", variant="surface", high_contrast=True),
        badge("New", variant="outline", high_contrast=True),
        gap="2",
    ),
    direction="column",
    gap="2",
)
```

### 半径

我们使用 `radius` 属性来分配特定的半径值，忽略全局主题。它可以取值为 `"none" | "small" | "medium" | "large" | "full"`。

```python demo
flex(
    badge("New", radius="none"),
    badge("New", radius="small"),
    badge("New", radius="medium"),
    badge("New", radius="large"),
    badge("New", radius="full"),
    gap="3",
)
```

## 最终示例

这是一个更高级的示例，展示如何在 `badge` 组件中使用图标。我们使用 `flex` 组件来正确对齐图标和文本，使用 `gap` 属性确保我们有正确的间距。

```python demo
badge(
    flex(icon(tag="arrow_up"),
        text("8.8%"),
        gap="1",
    ),
    color="grass",
)
```

