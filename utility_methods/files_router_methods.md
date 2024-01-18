# 状态工具方法

状态对象具有多个方法和属性，用于返回有关当前页面、会话或状态的信息。

## 文件路由器方法

`self.router` 属性具有多个子属性，提供各种信息:

* `router.page`: 当前页面和路由的数据
  * `host`: 提供当前页面的主机名和端口（前端）。
  * `path`: 当前页面的路径（对于动态页面，将包含 slug）
  * `raw_path`: 在浏览器中显示的页面路径（包括参数和动态值）
  * `full_path`: 使用 `host` 作为前缀的 `path`
  * `full_raw_path`: 使用 `host` 作为前缀的 `raw_path`
  * `params`: 与请求相关的查询参数字典

* `router.session`: 当前会话的数据
  * `client_token`: 与当前标签页令牌相关联的 UUID。每个标签页都有唯一的令牌。
  * `session_id`: 与客户端的 WebSocket 连接关联的 ID。每个标签页都有唯一的会话 ID。
  * `client_ip`: 客户端的 IP 地址。许多用户可能共享相同的 IP 地址。

* `router.headers`: 与 WebSocket 连接相关的一些常见标头的选择。这些值只能在重新建立 WebSocket 时更改（例如，在页面刷新期间）。所有其他标头都在字典 `self.router_data.headers` 中可用。
  * `host`: 提供 WebSocket 的主机名和端口（后端）。

### 本页上的示例值

```python demo exec
class RouterState(rx.State):
    pass


def router_values():
    return rx.table(
        headers=["Name", "Value"],
        rows=[
            [rx.text("router.page.host"), rx.code(RouterState.router.page.host)],
            [rx.text("router.page.path"), rx.code(RouterState.router.page.path)],
            [rx.text("router.page.raw_path"), rx.code(RouterState.router.page.raw_path)],
            [rx.text("router.page.full_path"), rx.code(RouterState.router.page.full_path)],
            [rx.text("router.page.full_raw_path"), rx.code(RouterState.router.page.full_raw_path)],
            [rx.text("router.page.params"), rx.code(RouterState.router.page.params.to_string())],
            [rx.text("router.session.client_token"), rx.code(RouterState.router.session.client_token)],
            [rx.text("router.session.session_id"), rx.code(RouterState.router.session.session_id)],
            [rx.text("router.session.client_ip"), rx.code(RouterState.router.session.client_ip)],
            [rx.text("router.headers.host"), rx.code(RouterState.router.headers.host)],
            [rx.text("router.headers.user_agent"), rx.code(RouterState.router.headers.user_agent)],
            [rx.text("router.headers.to_string()"), rx.code(RouterState.router.headers.to_string())],
        ],
        overflow_x="auto",
    )
```

