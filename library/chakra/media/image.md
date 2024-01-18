---

components:
    - rx.chakra.Image
---

```python exec
import reflex as rx
```

# 图片

Image组件可以通过`src`参数显示一张图片。这可以是来自资产文件夹的本地路径，也可以是外部链接。

```python demo
rx.image(src="/reflex_logo.png", width="100px", height="auto")
```

Image组件由一个盒子组成，可以进行样式化。

```python demo
rx.image(
    src="/reflex_logo.png",
    width="100px",
    height="auto",
    border_radius="15px 50px",
    border="5px solid #555",
    box_shadow="lg",
)
```

您还可以将`PIL`图像对象作为`src`参数传递。

```python demo box
rx.vstack(
    rx.image(src="https://picsum.photos/id/1/200/300", alt="An Unsplash Image")
)
```

```python
from PIL import Image
import requests


class ImageState(rx.State):
    url = f"https://picsum.photos/id/1/200/300"
    image = Image.open(requests.get(url, stream=True).raw)


def image_pil_example():
    return rx.vstack(
        rx.image(src=ImageState.image)
    )
```

