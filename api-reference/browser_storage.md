# 浏览器存储

## rx.Cookie

表示一个状态变量，以 cookie 的形式存储在浏览器中。目前仅支持字符串值。

参数
- `name`：cookie 在客户端的名称。
- `path`：cookie 的路径。使用 `/` 可让 cookie 在所有页面中访问。
- `max_age`：cookie 的相对最大生存期（以秒为单位），从客户端接收到 cookie 开始计时。
- `domain`：cookie 的域（例如 `sub.domain.com` 或 `.allsubdomains.com`）。
- `secure`：cookie 是否仅通过 HTTPS 访问。
- `same_site`：cookie 是否随第三方请求一起发送。可以是 `True`、`False`、`None`、`lax`、`strict` 中的一种。

```python
class CookieState(rx.State):
    c1: str = rx.Cookie()
    c2: str = rx.Cookie('c2 default')

    # cookies with custom settings
    c3: str = rx.Cookie(max_age=2)  # expires after 2 second
    c4: str = rx.Cookie(same_site='strict')
    c5: str = rx.Cookie(path='/foo/')  # only accessible on `/foo/`
    c6: str = rx.Cookie(name='c6-custom-name')
```

## rx.remove_cookies
从客户端浏览器中删除一个 cookie。

参数：
- `key`：要删除的 cookie 的名称。

```python
rx.button(
    'Remove cookie', on_click=rx.remove_cookie('key')
)
```

此事件也可以从事件处理程序返回：

```python
class CookieState(rx.State):
    ...
    def logout(self):
        return rx.remove_cookie('auth_token')
```

## rx.LocalStorage
表示一个状态变量，以 localStorage 的形式存储在浏览器中。目前仅支持字符串值。

参数
- `name`：在客户端的存储键的名称。

```python
class LocalStorageState(rx.State):
    # local storage with default settings
    l1: str = rx.LocalStorage()

    # local storage with custom settings
    l2: str = rx.LocalStorage("l2 default")
    l3: str = rx.LocalStorage(name="l3")
```

## rx.remove_local_storage
从客户端浏览器中删除一个本地存储项。

参数
- `key`：要从本地存储中删除的键。

```python
rx.button(
    'Remove Local Storage',
    on_click=rx.remove_local_storage('key'),
)
```

此事件也可以从事件处理程序返回：

```python
class LocalStorageState(rx.State):
    ...
    def logout(self):
        return rx.remove_local_storage('local_storage_state.l1')
```

## rx.clear_local_storage()

从客户端浏览器中清除所有本地存储项。这可能会影响在同一域中运行的其他应用程序或使用本地存储的应用程序库。

```python
rx.button(
    'Clear all Local Storage',
    on_click=rx.clear_local_storage(),
)
```

# 序列化策略

如果一个非平凡的数据结构应该存储在 `Cookie` 或 `LocalStorage` 变量中，则需要在存储之前和之后对其进行序列化。建议使用 `rx.Base` 处理数据，它提供了简单的序列化辅助函数，并能在复杂对象结构中进行递归处理。

```python demo exec
import reflex as rx


class AppSettings(rx.Base):
    theme: str = 'light'
    sidebar_visible: bool = True
    update_frequency: int = 60
    error_messages: list[str] = []


class ComplexLocalStorageState(rx.State):
    data_raw: str = rx.LocalStorage("{}")
    data: AppSettings = AppSettings()
    settings_open: bool = False

    def save_settings(self):
        self.data_raw = self.data.json()
        self.settings_open = False

    def open_settings(self):
        self.data = AppSettings.parse_raw(self.data_raw)
        self.settings_open = True

    def set_field(self, field, value):
        setattr(self.data, field, value)


def app_settings():
    return rx.form(
        rx.foreach(
            ComplexLocalStorageState.data.error_messages,
            rx.text,
        ),
        rx.form_label(
            "Theme",
            rx.input(
                value=ComplexLocalStorageState.data.theme,
                on_change=lambda v: ComplexLocalStorageState.set_field("theme", v),
            ),
        ),
        rx.form_label(
            "Sidebar Visible",
            rx.switch(
                is_checked=ComplexLocalStorageState.data.sidebar_visible,
                on_change=lambda v: ComplexLocalStorageState.set_field(
                    "sidebar_visible",
                    v,
                ),
            ),
        ),
        rx.form_label(
            "Update Frequency (seconds)",
            rx.number_input(
                value=ComplexLocalStorageState.data.update_frequency,
                on_change=lambda v: ComplexLocalStorageState.set_field(
                    "update_frequency",
                    v,
                ),
            ),
        ),
        rx.button("Save", type_="submit"),
        on_submit=lambda _: ComplexLocalStorageState.save_settings(),
    )

def app_settings_example():
    return rx.fragment(
        rx.modal(
            rx.modal_overlay(
                rx.modal_content(
                    rx.modal_header("App Settings"),
                    rx.modal_body(app_settings()),
                ),
            ),
            is_open=ComplexLocalStorageState.settings_open,
            on_close=ComplexLocalStorageState.set_settings_open(False),
        ),
        rx.button("App Settings", on_click=ComplexLocalStorageState.open_settings),
    )
```

