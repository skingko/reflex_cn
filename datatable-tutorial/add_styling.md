```python exec
import reflex as rx
from datatable_tutorial_utils import DataTableState, DataTableState2
```

# 数据表格样式


有一些属性我们可以探索，以确保数据表格的形状正确，并以我们预期的方式进行反应。我们可以将 `on_paste` 设置为 `True`，这样我们就可以直接将内容粘贴到单元格中。我们可以使用 `draw_focus_ring` 在选定单元格周围绘制一个环形，默认情况下为 `True`，如果不需要，可以关闭它。通过 `rows` 属性，我们可以硬编码显示的行数。

`freeze_columns` 用于在水平滚动时保持某些左侧列固定。`group_header_height` 和 `header_height` 分别定义了分组标题和各个表头的高度。`max_column_width` 和 `min_column_width` 定义了手动调整列宽的允许范围。我们还可以定义 `row_height` 以使行之间有更好的间距。

我们可以添加 `row_markers`，它们出现在表格的最左侧。它们可以取值为 `'none'、'number'、'checkbox'、'both'、'clickable-number'`。我们可以设置 `smooth_scroll_x` 和 `smooth_scroll_y`，这样就可以平滑地沿着列和行滚动。

默认情况下，列之间有一个`vertical_border`。我们可以将此属性设置为 `False` 来关闭它。我们可以通过设置 `column_select` 属性来定义用户一次可以选择多少列。它可以取值为 `"none"、"single"、"multi"`。

我们可以允许 `overscroll_x`，这样用户可以在实际水平内容限制之外滚动。还有一个对应的 `overscroll_y`。

请参考[这些文档](https://reflex.dev/docs/library/datadisplay/dataeditor/)，了解更多有关这些属性的信息。

```python demo
rx.data_editor(
    columns=DataTableState2.cols,
    data=DataTableState2.data,

    #rows=4,
    on_paste=True,
    draw_focus_ring=False,
    freeze_columns=2,
    group_header_height=50,
    header_height=60,
    max_column_width=300,
    min_column_width=100,
    row_height=50,
    row_markers='clickable-number',
    smooth_scroll_x=True,
    vertical_border=False,
    column_select="multi",
    overscroll_x=100,


    on_cell_clicked=DataTableState2.get_clicked_data,
    on_cell_edited=DataTableState2.get_edited_data,
    on_group_header_context_menu=DataTableState2.get_group_header_right_click,
    on_item_hovered=DataTableState2.get_item_hovered,
    on_delete=DataTableState2.get_deleted_item,
    on_column_resize=DataTableState2.column_resize,
)
```


## 主题

最后，有一个 `theme` 属性，可以用于传递数据表格的所有颜色和字体信息。

```python
darkTheme = {
    "accentColor": "#8c96ff",
    "accentLight": "rgba(202, 206, 255, 0.253)",
    "textDark": "#ffffff",
    "textMedium": "#b8b8b8",
    "textLight": "#a0a0a0",
    "textBubble": "#ffffff",
    "bgIconHeader": "#b8b8b8",
    "fgIconHeader": "#000000",
    "textHeader": "#a1a1a1",
    "textHeaderSelected": "#000000",
    "bgCell": "#16161b",
    "bgCellMedium": "#202027",
    "bgHeader": "#212121",
    "bgHeaderHasFocus": "#474747",
    "bgHeaderHovered": "#404040",
    "bgBubble": "#212121",
    "bgBubbleSelected": "#000000",
    "bgSearchResult": "#423c24",
    "borderColor": "rgba(225,225,225,0.2)",
    "drilldownBorder": "rgba(225,225,225,0.4)",
    "linkColor": "#4F5DFF",
    "headerFontStyle": "bold 14px",
    "baseFontStyle": "13px",
    "fontFamily": "Inter, Roboto, -apple-system, BlinkMacSystemFont, avenir next, avenir, segoe ui, helvetica neue, helvetica, Ubuntu, noto, arial, sans-serif",
}
```

```python exec
darkTheme = {
    "accentColor": "#8c96ff",
    "accentLight": "rgba(202, 206, 255, 0.253)",
    "textDark": "#ffffff",
    "textMedium": "#b8b8b8",
    "textLight": "#a0a0a0",
    "textBubble": "#ffffff",
    "bgIconHeader": "#b8b8b8",
    "fgIconHeader": "#000000",
    "textHeader": "#a1a1a1",
    "textHeaderSelected": "#000000",
    "bgCell": "#16161b",
    "bgCellMedium": "#202027",
    "bgHeader": "#212121",
    "bgHeaderHasFocus": "#474747",
    "bgHeaderHovered": "#404040",
    "bgBubble": "#212121",
    "bgBubbleSelected": "#000000",
    "bgSearchResult": "#423c24",
    "borderColor": "rgba(225,225,225,0.2)",
    "drilldownBorder": "rgba(225,225,225,0.4)",
    "linkColor": "#4F5DFF",
    "headerFontStyle": "bold 14px",
    "baseFontStyle": "13px",
    "fontFamily": "Inter, Roboto, -apple-system, BlinkMacSystemFont, avenir next, avenir, segoe ui, helvetica neue, helvetica, Ubuntu, noto, arial, sans-serif",
}
```

```python demo
rx.data_editor(
    columns=DataTableState2.cols,
    data=DataTableState2.data,

    on_paste=True,
    draw_focus_ring=False,
    freeze_columns=2,
    group_header_height=50,
    header_height=60,
    max_column_width=300,
    min_column_width=100,
    row_height=50,
    row_markers='clickable-number',
    smooth_scroll_x=True,
    vertical_border=False,
    column_select="multi",
    overscroll_x=100,
    theme=darkTheme,


    on_cell_clicked=DataTableState2.get_clicked_data,
    on_cell_edited=DataTableState2.get_edited_data,
    on_group_header_context_menu=DataTableState2.get_group_header_right_click,
    on_item_hovered=DataTableState2.get_item_hovered,
    on_delete=DataTableState2.get_deleted_item,
    on_column_resize=DataTableState2.column_resize,
)
```

