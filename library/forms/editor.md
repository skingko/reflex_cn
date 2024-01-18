---
components:
    - rx.Editor
---

基于[Suneditor](http://suneditor.com/sample/index.html)的HTML编辑器组件。

```python demo exec
import reflex as rx

from pcweb import styles
from pcweb.pages.docs.source import Source, generate_docs
from pcweb.templates.docpage import h2_comp


class EditorState(rx.State):
    content: str = "<p>Editor content</p>"

    def handle_change(self, content: str):
        """Handle the editor value change."""
        self.content = content


def editor_example():
    return rx.vstack(
        rx.editor(
            set_contents=EditorState.content,
            on_change=EditorState.handle_change,
        ),
        rx.box(
            rx.html(EditorState.content),
            border="1px dashed #ccc",
            border_radius="4px",
            width="100%",
        ),
    )
```

# EditorOptions

通过为`set_options`属性传递`rx.EditorOptions`的实例，可以自定义扩展选项和工具栏按钮。

```python exec
editor_options_source = Source(module=rx.EditorOptions)
```

```python eval
rx.fragment(
    h2_comp(text="Fields"),
    rx.box(rx.table(
        rx.thead(
            rx.tr(
                rx.th("Field"),
                rx.th("Description"),
            )
        ),
        rx.tbody(
            *[
                rx.tr(
                    rx.td(rx.code(field["name"], font_weight=styles.BOLD_WEIGHT)),
                    rx.td(field["description"]),
                )
                for field in editor_options_source.get_fields()
            ],
        ),
    ), style={"overflow": "auto"}),
)
```

```python eval
rx.box(height="2em")
```

`button_list`属性需要一个列表列表，其中每个子列表包含工具栏上形成一组的按钮的名称。字符 "/"可以用来代替子列表，在工具栏中表示换行。

`rx.EditorButtonList`中列举了一些有效的`button_list`选项，如下所示。

```python
class EditorButtonList(list, enum.Enum):

    BASIC = [
        ["font", "fontSize"],
        ["fontColor"],
        ["horizontalRule"],
        ["link", "image"],
    ]
    FORMATTING = [
        ["undo", "redo"],
        ["bold", "underline", "italic", "strike", "subscript", "superscript"],
        ["removeFormat"],
        ["outdent", "indent"],
        ["fullScreen", "showBlocks", "codeView"],
        ["preview", "print"],
    ]
    COMPLEX = [
        ["undo", "redo"],
        ["font", "fontSize", "formatBlock"],
        ["bold", "underline", "italic", "strike", "subscript", "superscript"],
        ["removeFormat"],
        "/",
        ["fontColor", "hiliteColor"],
        ["outdent", "indent"],
        ["align", "horizontalRule", "list", "table"],
        ["link", "image", "video"],
        ["fullScreen", "showBlocks", "codeView"],
        ["preview", "print"],
        ["save", "template"],
    ]
```

也可以使用这些名称自定义工具栏按钮列表，如下所示。

由于此示例使用与上面相同的状态，因此两个编辑器的内容是共享的，可以由任意一个进行修改。

```python demo
rx.editor(
    set_contents=EditorState.content,
    set_options=rx.EditorOptions(
        button_list=[
            ["font", "fontSize", "formatBlock"],
            ["fontColor", "hiliteColor"],
            ["bold", "underline", "italic", "strike", "subscript", "superscript"],
            ["removeFormat"],
            "/",
            ["outdent", "indent"],
            ["align", "horizontalRule", "list", "table"],
            ["link"],
            ["fullScreen", "showBlocks", "codeView"],
            ["preview", "print"],
        ]
    ),
    on_change=EditorState.handle_change,
)
```

有关按钮和选项的详细信息，请参阅[Suneditor README.md](https://github.com/JiHong88/suneditor/blob/master/README.md)。

```python eval
rx.box(height="5em")
```

