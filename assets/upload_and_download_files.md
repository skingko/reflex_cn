```python exec
import reflex as rx
```


# 文件

除了应用程序附带的任何资产外，许多网络应用程序通常需要接收或发送文件，无论您是要共享媒体，允许用户导入其数据还是导出某些后端数据。

在本节中，我们将介绍您在 Reflex 中处理文件所需的所有内容。

## 下载

如果您希望让应用程序的用户从服务器下载文件到他们的计算机上，Reflex 为您提供了两种方法。

### 使用常规链接

对于一些基本的用法，只需在 `rx.link` 中提供资源路径即可，单击链接将下载该资源。

```python demo
rx.link("Download", href="/reflex_logo.png")
```

### 使用 `rx.download` 事件

如果一个简单的链接不够，或者您想要从后端触发下载，可以使用 `rx.download` 事件。

```python demo
rx.button(
    "Download", 
    on_click=rx.download(url="/reflex_logo.png"),
)
```

`rx.download` 还可以让您指定要下载的文件的名称，如果您希望它与服务器端的名称不同。

```python demo
rx.button(
    "Download and Rename", 
    on_click=rx.download(
        url="/reflex_logo.png", 
        filename="different_name_logo.png"
    ),
)
```

`rx.download` 的参考页面位于[此处]({"/docs/api-reference/special-events"})。

## 上传

将文件上载到服务器可以让用户以与仅填写表单提供数据不同的方式与应用程序交互。

组件 `rx.upload` 允许用户将文件上传到服务器。

以下是其基本用法示例：
```python
def index():
    return rx.fragment(
        rx.upload(rx.text("Upload files"), rx.icon(tag="upload")),
        rx.button(on_submit=State.<your_upload_handler>)
    )
```

有关详细信息，请参阅组件的参考页面[此处](/docs/library/forms/upload)。

