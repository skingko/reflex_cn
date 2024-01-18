```python exec
import reflex as rx
from pcweb import constants, styles

route = (
"""
@rx.page()
def index():
    return rx.text('Root Page')

@rx.page()
def about():
    return rx.text('About Page')

@rx.page(route='/custom-route')
def custom():
    return rx.text('Custom Route')

app = rx.App()
"""
)

nested_routes = (
"""
@rx.page(route='/nested/page')
def nested_page():
    return rx.text('Nested Page')

app = rx.App()
"""

)

  
routes_get_query_params = (
"""
class State(rx.State):
    @rx.var
    def user_post(self) -> str:
        args = self.router.page.params
        username = args.get('username')
        post_id = args.get('id')
        return f'Posts by {username}: Post {post_id}'

@rx.page(route='/user/[username]/posts/[id]')
def post():
    return rx.center(
        rx.text(State.user_post)
    )


app = rx.App()
"""  
)


page_decorator = (
"""
@rx.page(route='/', title='My Beautiful App')
def index():
    return rx.text('A Beautiful App')
"""  
)

current_page_link = (
"""
class State(rx.State):
    
    @rx.var
    def current_url(self) -> str:
        return self.router.page.full_raw_path
"""  
)


current_page_info = (
"""
class State(rx.State):
    def some_method(self):
        current_page_route = self.router.page.path
        current_page_url = self.router.page.raw_path
        # ... Your logic here ...

"""  
)

client_ip = (
"""
class State(rx.State):
    def some_method(self):
        client_ip = self.router.session.client_ip
        # ... Your logic here ...

"""  
)
```

# 页面
Reflex中的页面允许您为不同的网址定义组件。本节介绍创建页面、处理网址参数、访问查询参数、管理页面元数据和处理页面加载事件的方法。

## 添加页面
您可以通过定义一个返回组件的函数来创建页面。
默认情况下，函数名称将用作路由，但您也可以指定一个路由。

```python
{route.strip()}
```

在此示例中，我们创建了三个页面：
- `index` - 根路由，位于`/`处
- `about` - 位于`/about`处
- `/custom` - 位于`/custom-route`处

## 页面装饰器
您还可以使用`@rx.page`装饰器添加页面。

```python
{page_decorator}
```

这等效于使用相同参数调用`app.add_page`。

```md alert
# Index is a special exception where it is available at both `/` and `/index`. All other pages are only available at their specified route.
```

## 嵌套路由
页面还可以有嵌套路由。

```python
{nested_routes}
```
此组件将在`/nested/page`处可用。



## 获取当前页面链接
`router.page.path`属性允许您从路由数据中获取当前页面的路径，在动态页面中，这将包含slug而不是用于加载页面的实际值。

要获取浏览器中显示的实际URL，请使用`router.page.raw_path`。这将包含所有查询参数和动态路径段。

```python
{current_page_info}
```
在上面的示例中，`current_page_route`将包含路由模式（例如`/posts/[id]`），而`current_page_url`将包含实际URL（例如`http://example.com/posts/123`）。

要获取完整的URL，请使用`full_`前缀访问相同的属性。

示例：

```python
{current_page_link}
```
在此示例中，运行在`localhost`上将显示`http://localhost:3000/user/hey/posts/3/`


## 获取客户端IP
您可以使用`router.session.client_ip`属性来获取与当前状态关联的客户端的IP地址。

```python
{client_ip}
```

