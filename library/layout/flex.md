---

组件:
  - rx.radix.themes.Flex
---

```python exec
import reflex as rx
import reflex.components.radix.themes as rdxt
```

# Flex

Flex组件用于创建[flexbox布局](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/CSS_layout/Flexbox)。
它简化了在水平或垂直方向上排列子组件、应用换行、对齐内容以及根据可用空间自动调整组件大小的过程，非常适合构建响应式布局。

默认情况下，子组件水平排列(`direction="row"`)，不换行。

## 基本示例

```python demo
rdxt.flex(
    rdxt.card("Card 1"),
    rdxt.card("Card 2"),
    rdxt.card("Card 3"),
    rdxt.card("Card 4"),
    rdxt.card("Card 5"),
    gap="2",
    width="100%",
)
```

## 换行

使用`flex_wrap="wrap"`，子组件将换行而不是被调整大小。

```python demo
rdxt.flex(
    rx.foreach(
        rx.Var.range(10),
        lambda i: rdxt.card(f"Card {i + 1}", width="16%"),
    ),
    gap="2",
    flex_wrap="wrap",
    width="100%",
)
```

## 方向

使用`direction="column"`，子组件将垂直排列。

```python demo
rdxt.flex(
    rdxt.card("Card 1"),
    rdxt.card("Card 2"),
    rdxt.card("Card 3"),
    rdxt.card("Card 4"),
    gap="2",
    direction="column",
)
```

## 对齐

两个属性控制子组件在Flex组件内的对齐方式：

* `align` 控制子组件沿交叉轴（对`row`来说是垂直的，对`column`来说是水平的）的对齐方式。
* `justify` 控制子组件沿主轴（对`row`来说是水平的，对`column`来说是垂直的）的对齐方式。

下面的示例通过不同的`wrap`和`direction`值可视化地展示了这些属性的效果。

```python demo exec
class FlexPlaygroundState(rx.State):
    align: str = "stretch"
    justify: str = "start"
    direction: str = "row"
    wrap: str = "nowrap"
    
    
def select(label, items, value, on_value_change):
    return rdxt.flex(
        rdxt.text(label),
        rdxt.select_root(
            rdxt.select_trigger(),
            rdxt.select_content(
                *[
                    rdxt.select_item(item, value=item)
                    for item in items
                ]
            ),
            value=value,
            on_value_change=on_value_change,
        ),
        align="center",
        justify="center",
        direction="column",
    )


def selectors():
    return rdxt.flex(
        select("Wrap", ["nowrap", "wrap", "wrap-reverse"], FlexPlaygroundState.wrap, FlexPlaygroundState.set_wrap),
        select("Direction", ["row", "column", "row-reverse", "column-reverse"], FlexPlaygroundState.direction, FlexPlaygroundState.set_direction),
        select("Align", ["start", "center", "end", "baseline", "stretch"], FlexPlaygroundState.align, FlexPlaygroundState.set_align),
        select("Justify", ["start", "center", "end", "between"], FlexPlaygroundState.justify, FlexPlaygroundState.set_justify),
        width="100%",
        gap="2",
        justify="between",
    )


def example1():
    return rdxt.box(
        selectors(),
        rdxt.flex(
            rx.foreach(
                rx.Var.range(10),
                lambda i: rdxt.card(f"Card {i + 1}", width="16%"),
            ),
            gap="2",
            direction=FlexPlaygroundState.direction,
            align=FlexPlaygroundState.align,
            justify=FlexPlaygroundState.justify,
            wrap=FlexPlaygroundState.wrap,
            width="100%",
            height="20vh",
            mt="4",
        ),
        width="100%",
    )
```


## 尺寸提示

当将子组件包含在Flex容器中时，`grow` (默认为`"0"`) 和 `shrink` (默认为`"1"`) 控制盒子相对于同一容器中的其他组件的大小。

调整大小始终应用于Flex容器的主轴。如果方向为`row`，则大小适用于`宽度`。如果方向为`column`，则大小适用于`高度`。为了设置主轴上的最佳大小，使用`flex_basis`属性，该属性可以是百分比或CSS尺寸单位。如果未指定，将使用对应的`宽度`或`高度`值（如果已设置），否则将使用内容大小。

当`grow="0"`时，盒子的大小不会超过`flex_basis`。

当`shrink="0"`时，盒子的大小不会缩小到小于`flex_basis`。

这些属性用于创建灵活的响应式布局。

移动下方的滑块，观察调整Flex容器的宽度如何影响基于设置的属性的Flex项的计算大小。

```python demo exec
class FlexGrowShrinkState(rx.State):
    width_pct: list[int] = [100]
    
    
def border_box(*children, **props):
    return rdxt.box(
        *children,
        border="1px solid var(--gray-10)",
        border_radius="2px",
        **props,
    )

    
def example2():
    return rdxt.box(
        rdxt.flex(
            border_box("shrink=0", shrink="0", width="100px"),
            border_box("shrink=1", shrink="1", width="200px"),
            border_box("grow=0", grow="0"),
            border_box("grow=1", grow="1"),
            width=f"{FlexGrowShrinkState.width_pct}%",
            mb="4",
            gap="2",
        ),
        rdxt.slider(
            min=0,
            max=100,
            value=FlexGrowShrinkState.width_pct,
            on_value_change=FlexGrowShrinkState.set_width_pct,
        ),
        width="100%",
    )
```

