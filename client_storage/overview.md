```python exec
import reflex as rx
```



# 客户端存储

您可以使用浏览器的本地存储来在会话之间保持状态。这可以让用户偏好设置、身份验证 cookie 和其他信息被存储在客户端，并在不同的浏览器标签中访问。

一个客户端存储变量的外观和行为与普通的 `str` 变量相似，只不过默认值是根据应该存储值的位置分别是 `rx.Cookie` 或 `rx.LocalStorage`。键名将基于变量名，但可以通过传递 `name="my_custom_name"` 作为关键字参数来覆盖键名。

了解更多信息请参见 [浏览器存储](/docs/api-reference/browser/)。

在下面的文本框中输入一些值，然后在单独的标签页中加载页面或检查浏览器开发工具的存储部分，以查看保存在浏览器中的值。

```python demo exec
class ClientStorageState(rx.State):
    my_cookie: str = rx.Cookie("")
    my_local_storage: str = rx.LocalStorage("")
    custom_cookie: str = rx.Cookie(name="CustomNamedCookie", max_age=3600)


def client_storage_example():
    return rx.vstack(
        rx.hstack(rx.text("my_cookie"), rx.input(value=ClientStorageState.my_cookie, on_change=ClientStorageState.set_my_cookie)),
        rx.hstack(rx.text("my_local_storage"), rx.input(value=ClientStorageState.my_local_storage, on_change=ClientStorageState.set_my_local_storage)),
        rx.hstack(rx.text("custom_cookie"), rx.input(value=ClientStorageState.custom_cookie, on_change=ClientStorageState.set_custom_cookie)),
    )
```

