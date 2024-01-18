```python exec
import reflex as rx
```

# 后端 API 路由

除了前端应用程序外，Reflex 还使用 FastAPI 后端来提供应用程序的服务。

要向后端 API 添加额外的端点，可以使用 `app.add_api_route` 并添加一个返回 JSON 的路由。

```python
async def api_test(item_id: int):
    return \{"my_result": item_id}

app = rx.App()
app.api.add_api_route("/items/\{item_id}", api_test)
```

现在，您可以访问 `localhost:8000/items/23` 端点并获得结果。

这对于创建一个可用于 Reflex 应用以外目的的后端 API 非常有用。

## 保留路由

后端的一些路由是为 Reflex 的运行时所保留的，除非您知道自己在做什么，否则不应该对其进行覆盖。

## Ping

`localhost:8000/ping/`：您可以使用此路由来检查后端的健康状况。

预期返回结果是 `"pong"`。

## Event

`localhost:8000/_event`：前端将使用此路由通知后端发生了一个事件。

```md alert error
# Overriding this route will break the event communication
```

## Upload

`localhost:8000/_upload`：这个路由用于在使用 `rx.upload()` 时上传文件。

