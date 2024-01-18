---
components:
    - rx.DataEditor
---

基于[Glide Data Grid](https://grid.glideapps.com/)的数据网格编辑器。

```python exec
import reflex as rx
from typing import Any

columns: list[dict[str, str]] = [
    {
        "title":"Code",
        "type": "str",
    },
    {
        "title":"Value",
        "type": "int",
    }, 
    {
        "title":"Activated",
        "type": "bool",
    },
]
data: list[list[Any]] = [
    ["A", 1, True],
    ["B", 2, False],
    ["C", 3, False],
    ["D", 4, True],
    ["E", 5, True],
    ["F", 6, False],
]

```

此组件是作为[datatable](docs/library/datadisplay/datatable)的替代方案引入的，用于支持对显示的数据进行编辑。



## 列

列的定义应为`list`包含多个`dict`，每个`dict`描述了对应的列。
列dict的属性：
- `title`：列标题显示的文本。
- `id`：列的id，如果未定义，则默认为`title`的小写形式。
- `width`：列的宽度。
- `type`：列的类型，默认为`"str"`。

## 数据

`rx.data_editor`的`data`属性接受一个`list`包含多个`list`，其中每个`list`表示要在表格中显示的一行数据。


## 简单示例

这是一个使用`data_editor`表示没有交互和样式的数据的基本示例。下面我们定义了传递给`rx.data_editor`组件的`columns`和`data`。在定义`columns`时，我们必须为每个列定义`title`和`type`。`data`中的列必须匹配定义的`type`，否则将会出错。

```python demo box
rx.data_editor(
    columns=columns,
    data=data,
)
```

```python
columns: list[dict[str, str]] = [
    {
        "title":"Code",
        "type": "str",
    },
    {
        "title":"Value",
        "type": "int",
    }, 
    {
        "title":"Activated",
        "type": "bool",
    },
]
data: list[list[Any]] = [
    ["A", 1, True],
    ["B", 2, False],
    ["C", 3, False],
    ["D", 4, True],
    ["E", 5, True],
    ["F", 6, False],
]
```

```python
rx.data_editor(
    columns=columns,
    data=data,
)
```

## 交互示例

```python exec
class DataEditorState_HP(rx.State):

    clicked_data: str = "Cell clicked: "
    cols: list[Any] = [
        {"title": "Title", "type": "str"},
        {
            "title": "Name",
            "type": "str",
            "group": "Data",
            "width": 300,
        },
        {
            "title": "Birth",
            "type": "str",
            "id": "date",
            "group": "Data",
            "width": 150,
        },
        {
            "title": "Human",
            "type": "bool",
            "group": "Data",
            "width": 80,
        },
        {
            "title": "House",
            "type": "str",
            "id": "date",
            "group": "Data",
        },
        {
            "title": "Wand",
            "type": "str",
            "id": "date",
            "group": "Data",
            "width": 250,
        },
        {
            "title": "Patronus",
            "type": "str",
            "id": "date",
            "group": "Data",
        },
        {
            "title": "Blood status",
            "type": "str",
            "id": "date",
            "group": "Data",
            "width": 200,
        }
    ]

    data = [
        ["1", "Harry James Potter",	"31 July 1980", True, "Gryffindor", "11'  Holly  phoenix feather", "Stag", "Half-blood"],
        ["2", "Ronald Bilius Weasley", "1 March 1980", True,"Gryffindor", "12' Ash unicorn tail hair", "Jack Russell terrier", "Pure-blood"],
        ["3", "Hermione Jean Granger", "19 September, 1979", True, "Gryffindor", "10¾'  vine wood dragon heartstring", "Otter", "Muggle-born"],	
        ["4", "Albus Percival Wulfric Brian Dumbledore", "Late August 1881", True, "Gryffindor", "15' Elder Thestral tail hair core", "Phoenix", "Half-blood"],	
        ["5", "Rubeus Hagrid", "6 December 1928", False, "Gryffindor", "16'  Oak unknown core", "None", "Part-Human (Half-giant)"], 
        ["6", "Fred Weasley", "1 April, 1978", True, "Gryffindor", "Unknown", "Unknown", "Pure-blood"], 
    ]

    def click_cell(self, pos):
        col, row = pos
        yield self.get_clicked_data(pos)
        

    def get_clicked_data(self, pos) -> str:
        self.clicked_data = f"Cell clicked: {pos}"
        
```


在这里，我们定义了一个状态（如下所示），当我们单击单元格时，使用`on_cell_clicked`事件触发器将单元格的位置打印为标题。请查看此页面底部可以使用的所有其他数据表的事件触发器。我们还定义了一个具有标签为`Data`的`group`。这将以表格形式显示具有此`group`标签的所有列，该`group`将放在一个较大的`Data`组下。

```python demo box
rx.heading(DataEditorState_HP.clicked_data)
```

```python demo box
rx.data_editor(
    columns=DataEditorState_HP.cols,
    data=DataEditorState_HP.data,
    on_cell_clicked=DataEditorState_HP.click_cell,
)
```

```python
class DataEditorState_HP(rx.State):
    
    clicked_data: str = "Cell clicked: "

    cols: list[Any] = [
        {
            "title": "Title", 
            "type": "str"
        },
        {
            "title": "Name",
            "type": "str",
            "group": "Data",
            "width": 300,
        },
        {
            "title": "Birth",
            "type": "str",
            "group": "Data",
            "width": 150,
        },
        {
            "title": "Human",
            "type": "bool",
            "group": "Data",
            "width": 80,
        },
        {
            "title": "House",
            "type": "str",
            "group": "Data",
        },
        {
            "title": "Wand",
            "type": "str",
            "group": "Data",
            "width": 250,
        },
        {
            "title": "Patronus",
            "type": "str",
            "group": "Data",
        },
        {
            "title": "Blood status",
            "type": "str",
            "group": "Data",
            "width": 200,
        }
    ]

    data = [
        ["1", "Harry James Potter",	"31 July 1980", True, "Gryffindor", "11'  Holly  phoenix feather", "Stag", "Half-blood"],
        ["2", "Ronald Bilius Weasley", "1 March 1980", True,"Gryffindor", "12' Ash unicorn tail hair", "Jack Russell terrier", "Pure-blood"],
        ["3", "Hermione Jean Granger", "19 September, 1979", True, "Gryffindor", "10¾'  vine wood dragon heartstring", "Otter", "Muggle-born"],	
        ["4", "Albus Percival Wulfric Brian Dumbledore", "Late August 1881", True, "Gryffindor", "15' Elder Thestral tail hair core", "Phoenix", "Half-blood"],	
        ["5", "Rubeus Hagrid", "6 December 1928", False, "Gryffindor", "16'  Oak unknown core", "None", "Part-Human (Half-giant)"], 
        ["6", "Fred Weasley", "1 April, 1978", True, "Gryffindor", "Unknown", "Unknown", "Pure-blood"], 
    ]


    def click_cell(self, pos):
        col, row = pos
        yield self.get_clicked_data(pos)
        

    def get_clicked_data(self, pos) -> str:
        self.clicked_data = f"Cell clicked: \{pos}"
```

```python
rx.data_editor(
    columns=DataEditorState_HP.cols,
    data=DataEditorState_HP.data,
    on_cell_clicked=DataEditorState_HP.click_cell,
)
```


## 样式示例

现在让我们给数据表添加样式，使其看起来更美观和易于使用。我们首先导入`DataEditorTheme`，然后我们可以开始设置我们的样式属性，如下所示在`dark_theme`中。

然后我们使用`theme=DataEditorTheme(**dark_theme)`来设置这些主题。在样式之上，我们还可以设置一些`props`来进行其他的美化更改。我们将`row_height`设置为`50`，以使内容更易于阅读。我们还将`smooth_scroll_x`和`smooth_scroll_y`设置为`True`，以便我们可以平滑地在列和行之间滚动。最后，我们添加了`column_select=single`，其中column select可以取以下任意值：`none`、`single`或`multiple`。

```python exec
from reflex.components.datadisplay.dataeditor import DataEditorTheme
dark_theme = {
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


```python demo box
rx.data_editor(
    columns=DataEditorState_HP.cols,
    data=DataEditorState_HP.data,
    row_height=80,
    smooth_scroll_x=True,
    smooth_scroll_y=True,
    column_select="single",
    theme=DataEditorTheme(**dark_theme),
    height="30vh",
)
```

```python
from reflex.components.datadisplay.dataeditor import DataEditorTheme
dark_theme_snake_case = {
    "accent_color": "#8c96ff",
    "accent_light": "rgba(202, 206, 255, 0.253)",
    "text_dark": "#ffffff",
    "text_medium": "#b8b8b8",
    "text_light": "#a0a0a0",
    "text_bubble": "#ffffff",
    "bg_icon_header": "#b8b8b8",
    "fg_icon_header": "#000000",
    "text_header": "#a1a1a1",
    "text_header_selected": "#000000",
    "bg_cell": "#16161b",
    "bg_cell_medium": "#202027",
    "bg_header": "#212121",
    "bg_header_has_focus": "#474747",
    "bg_header_hovered": "#404040",
    "bg_bubble": "#212121",
    "bg_bubble_selected": "#000000",
    "bg_search_result": "#423c24",
    "border_color": "rgba(225,225,225,0.2)",
    "drilldown_border": "rgba(225,225,225,0.4)",
    "link_color": "#4F5DFF",
    "header_font_style": "bold 14px",
    "base_font_style": "13px",
    "font_family": "Inter, Roboto, -apple-system, BlinkMacSystemFont, avenir next, avenir, segoe ui, helvetica neue, helvetica, Ubuntu, noto, arial, sans-serif",
}
```


```python
rx.data_editor(
    columns=DataEditorState_HP.cols,
    data=DataEditorState_HP.data,
    row_height=80,
    smooth_scroll_x=True,
    smooth_scroll_y=True,
    column_select="single",
    theme=DataEditorTheme(**dark_theme),
    height="30vh",
)
```

