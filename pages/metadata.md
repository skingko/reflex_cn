```python exec

import reflex as rx

meta_data = (
"""
@rx.page(
    title='My Beautiful App',
    description='A beautiful app built with Reflex',
    image='/splash.png',
    meta=meta,
)
def index():
    return rx.text('A Beautiful App')

@rx.page(title='About Page')
def about():
    return rx.text('About Page')


meta = [
    {'name': 'theme_color', 'content': '#FFFFFF'},
    {'char_set': 'UTF-8'},
    {'property': 'og:url', 'content': 'url'},
]

app = rx.App()
"""  

)

```


# 页面元数据
您可以添加页面元数据，例如：

- 在浏览器标签中显示的标题
- 在搜索结果中显示的描述
- 在社交媒体上分享页面时显示的预览图像
- 任何额外的元数据

```python
{meta_data}
```

