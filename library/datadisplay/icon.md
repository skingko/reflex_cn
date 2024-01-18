```Chinese
---
components:
    - rx.radix.themes.Icon
---
# 图标

```python exec
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.components.icons import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
from pcweb.templates.docpage import icon_grid
```

图标组件用于显示一组图标中的某一个。此实现基于 [Radix 图标库](https://www.radix-ui.com/icons)。

## 基本示例

要创建一个图标，我们需要通过 `tag` 属性从可用的图标列表中指定。

```python demo
icon(tag="calendar")
```

## 图标列表

### 抽象

```python eval
icon_grid("Abstract", ICON_ABSTRACT)
```

### 对齐

```python eval
icon_grid("Alignment", ICON_ALIGNS, columns="3")
```

### 箭头

```python eval
icon_grid("Arrows", ICON_ARROWS)
```

### 边框和角落

```python eval
icon_grid("Borders and Corners", ICON_BORDERS)
```

### 设计

```python eval
icon_grid("Design", ICON_DESIGN)
```

### 组件

```python eval
icon_grid("Components", ICON_COMPONENTS, columns="5")
```

### 徽标

```python eval
icon_grid("Logos", ICON_LOGOS)
```

### 音乐

```python eval
icon_grid("Music", ICON_MUSIC)
```

### 物体

```python eval
icon_grid("Objects", ICON_OBJECTS)
```

### 排版

```python eval
icon_grid("Typography", ICON_TYPOGRAPHY)
```

## 样式

这些图标基于 Radix 原始组件，没有任何样式。**它不接受常见的样式属性，如 `size` 或 `color_theme`**。您仍然可以通过同时使用 `width` 和 `height` 来控制图标的大小，并指定它的 `color`。

### 宽度和高度

```python demo
flex(
    icon(tag="magnifying_glass", width=15, height=15),
    icon(tag="magnifying_glass", width=20, height=20),
    icon(tag="magnifying_glass", width=25, height=25),
    icon(tag="magnifying_glass", width=30, height=30),
    align="center",
    gap="2",
)
```

## 颜色

这是一个使用基本颜色的图标示例。

```python demo
flex(
    icon(tag="magnifying_glass", width=18, height=18, color="indigo"),
    icon(tag="magnifying_glass", width=18, height=18, color="cyan"),
    icon(tag="magnifying_glass", width=18, height=18, color="orange"),
    icon(tag="magnifying_glass", width=18, height=18, color="crimson"),
    gap="2",
)
```

您还可以使用包含颜色比例的颜色。

```python demo
flex(
    icon(tag="magnifying_glass", width=18, height=18, color="var(--purple-1)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--purple-2)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--purple-3)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--purple-4)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--purple-5)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--purple-6)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--purple-7)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--purple-8)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--purple-9)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--purple-10)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--purple-11)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--purple-12)"),
    gap="2",
)
```

这是另一个示例，使用了带有比例的 `accent` 颜色。`accent` 是您主题中最重要的颜色。

```python demo
flex(
    icon(tag="magnifying_glass", width=18, height=18, color="var(--accent-1)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--accent-2)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--accent-3)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--accent-4)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--accent-5)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--accent-6)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--accent-7)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--accent-8)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--accent-9)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--accent-10)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--accent-11)"),
    icon(tag="magnifying_glass", width=18, height=18, color="var(--accent-12)"),
    gap="2",
)
```

## 最终示例

图标可以作为其他许多组件的子组件使用。这是一个包含放大镜图标的搜索栏示例。

```python demo
badge(
    flex(
        icon(tag="magnifying_glass", height=18, width=18),
        text("Search documentation...", size="3", weight="medium"),
        direction="row",
        gap="1",
        align="center",
    ),
    size="2",
    radius="full",
    color_scheme="gray",
)
```
```

