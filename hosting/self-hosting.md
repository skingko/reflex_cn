# 自己托管

如果可用，我们建议使用 `reflex deploy`，但是您也可以在此期间自行托管您的应用程序。

将代码克隆到服务器，并安装 [requirements]({getting_started.installation.path})。

## API URL
编辑您的 `rxconfig.py` 文件，并将 `api_url` 设置为服务器的公共可访问 IP 地址或主机名，并在末尾加上端口 `:8000`。正确设置此项对于前端与后端状态的交互至关重要。

例如，如果您的服务器位于 `app.example.com`，您的配置将如下所示：

```python
```python
config = rx.Config(
    app_name="your_app_name",
    api_url="http://app.example.com:8000",
)
```
```

您也可以在运行时或导出时设置环境变量 `API_URL`，以保留本地开发的默认值。

## 生产模式

然后以生产模式运行您的应用程序：

```bash
```bash
reflex run --env prod
```
```

生产模式将创建应用程序的优化构建版。默认情况下，应用程序的静态前端（HTML、Javascript、CSS）将暴露在端口 `3000` 上，后端（事件处理程序）将监听端口 `8000`。

```python
```md alert warning
# Reverse Proxy and Websockets
Because the backend uses websockets, some reverse proxy servers, like [nginx](https://nginx.org/en/docs/http/websocket.html) or [apache](https://httpd.apache.org/docs/2.4/mod/mod_proxy.html#protoupgrade), must be configured to pass the `Upgrade` header to allow backend connectivity.
```
```

## 导出静态构建

导出前端的静态构建允许使用静态托管提供者（如 Netlify 或 Github Pages）来提供应用程序。在导出前端时，请确保 `api_url` 已设置为可访问的后端 URL。

```bash
```bash
API_URL=http://app.example.com:8000 reflex export
```
```

这将创建一个名为 `frontend.zip` 的文件，其中包含应用程序的缩小版 HTML、Javascript 和 CSS 构建，可上传到您的静态托管服务。

它还会创建一个名为 `backend.zip` 的文件，其中包含应用程序的后端 Python 代码，可上传到服务器并运行。

您可以通过传入 `--frontend-only` 或 `--backend-only` 标志来仅导出前端或后端。

还可以将组件导出而不压缩。要这样做，请使用 `--no-zip` 参数。这会将前端放置在 `.web/_static/` 目录中，而后端可以在项目的根目录中找到。

## Reflex 容器服务

另一种选择是在容器中运行 Reflex 服务。为此，Reflex 项目中的 `docker-example` 目录中提供了一个 `Dockerfile` 和其他文档。

在构建容器映像时，您需要编辑 `rxconfig.py`，并将 `requirements.txt` 添加到您的项目文件夹中。在 `rxconfig.py` 中需要进行以下更改：

```python
```python
config = rx.Config(
    app_name="app",
    api_url="http://app.example.com:8000",
)
```
```
请注意，`api_url` 应设置为外部可访问的主机名或 IP，因为客户端浏览器必须能够直接连接到它以建立交互性。

您还可以在项目的 `docker-example` 文件夹中找到 `requirements.txt`。

项目结构应如下所示：

```bash
```bash
hello
├── .web
├── assets
├── hello
│   ├── __init__.py
│   └── hello.py
├── rxconfig.py
├── Dockerfile
└── requirements.txt
```
```

完成所有更改后，现在可以创建容器映像，如下所示。

```bash
```bash
docker build -t reflex-project:latest .
```
```

最后，您可以启动 Reflex 容器服务，如下所示。

```bash
```bash
docker run -d -p 3000:3000 -p 8000:8000 --name app reflex-project:latest
```
```

