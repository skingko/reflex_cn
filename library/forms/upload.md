---

components:
    - rx.Upload
---

```python exec
import reflex as rx
```

# 上传

Upload组件可以用来上传文件到服务器。

你可以通过传递子组件来自定义其外观。
你可以通过点击组件或将文件拖放到组件上来上传文件。

```python demo
rx.upload(
    rx.text("Drag and drop files here or click to select files"),
    border="1px dotted rgb(107,99,246)",
    padding="5em",
)
```

选择文件将其添加到浏览器的文件列表中，可以使用`rx.selected_files`特殊变量在前端渲染。
要清除所选文件，可以使用另一个特殊变量`rx.clear_selected_files`作为事件处理器。
要上传文件，需要绑定一个事件处理器并传递文件列表。

下面是一个完整的示例。

```python demo box
rx.image(src="/upload.gif")
```

```python
class State(rx.State):
    \"""The app state.\"""

    # The images to show.
    img: list[str]

    async def handle_upload(self, files: list[rx.UploadFile]):
        \"""Handle the upload of file(s).

        Args:
            files: The uploaded files.
        \"""
        for file in files:
            upload_data = await file.read()
            outfile = rx.get_asset_path(file.filename)

            # Save the file.
            with open(outfile, "wb") as file_object:
                file_object.write(upload_data)

            # Update the img var.
            self.img.append(file.filename)


color = "rgb(107,99,246)"


def index():
    \"""The main view.\"""
    return rx.vstack(
        rx.upload(
            rx.vstack(
                rx.button("Select File", color=color, bg="white", border=f"1px solid \{color}"),
                rx.text("Drag and drop files here or click to select files"),
            ),
            border=f"1px dotted \{color}",
            padding="5em",
        ),
        rx.hstack(rx.foreach(rx.selected_files, rx.text)),
        rx.button(
            "Upload",
            on_click=lambda: State.handle_upload(rx.upload_files()),
        ),
        rx.button(
            "Clear",
            on_click=rx.clear_selected_files,
        ),
        rx.foreach(State.img, lambda img: rx.image(src=img)),
        padding="5em",
    )
```

在下面的示例中，上传组件接受最多5个特定类型的文件。
它还禁用了使用空格键或回车键上传文件。

```python
class State(rx.State):
    \"""The app state.\"""

    # The images to show.
    img: list[str]

    async def handle_upload(self, files: list[rx.UploadFile]):
        \"""Handle the upload of file(s).

        Args:
            files: The uploaded files.
        \"""
        for file in files:
            upload_data = await file.read()
            outfile = f".web/public/\{file.filename}"

            # Save the file.
            with open(outfile, "wb") as file_object:
                file_object.write(upload_data)

            # Update the img var.
            self.img.append(file.filename)


color = "rgb(107,99,246)"


def index():
    \"""The main view.\"""
    return rx.vstack(
        rx.upload(
            rx.vstack(
                rx.button("Select File", color=color, bg="white", border=f"1px solid \{color}"),
                rx.text("Drag and drop files here or click to select files"),
            ),
            multiple=True,
            accept = {
                "application/pdf": [".pdf"],
                "image/png": [".png"],
                "image/jpeg": [".jpg", ".jpeg"],
                "image/gif": [".gif"],
                "image/webp": [".webp"],
                "text/html": [".html", ".htm"],
            },
            max_files=5,
            disabled=False,
            on_keyboard=True,
            border=f"1px dotted \{color}",
            padding="5em",
        ),
        rx.button(
            "Upload",
            on_click=lambda: State.handle_upload(rx.upload_files()),
        ),
        rx.responsive_grid(
            rx.foreach(
                State.img,
                lambda img: rx.vstack(
                    rx.image(src=img),
                    rx.text(img),
                ),
            ),
            columns=[2],
            spacing="5px",
        ),
        padding="5em",
    )
```

你的事件处理器应该是一个接受单个参数`files: list[UploadFile]`的异步函数，其中将包含[FastAPI UploadFile](https://fastapi.tiangolo.com/tutorial/request-files)实例。
你可以读取文件并根据示例保存在任何位置。

在你的用户界面中，你可以将事件处理器绑定到触发器上，比如一个按钮的`on_click`事件，并使用`rx.upload_files()`传入文件。

