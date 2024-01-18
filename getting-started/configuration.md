```
```python exec
config_api_ref_url = "/docs/api-reference/config"
cli_api_ref_url = "/docs/api-reference/cli"
```

# 配置

Reflex 应用可以通过配置文件、环境变量和命令行参数进行配置。

## 配置文件

运行 `reflex init` 命令将在根目录下创建一个 `rxconfig.py` 文件。
您可以向 `Config` 类传递关键字参数来配置您的应用程序。

例如：

```python
# rxconfig.py
import reflex as rx

config = rx.Config(
    app_name="my_app_name",
    # Connect to your own database.
    db_url="postgresql://user:password@localhost:5432/my_db",
    # Change the frontend port.
    frontend_port=3001,
)
```

请参阅[配置参考]({config_api_ref_url})以获取所有可用的参数。

## 环境变量

您可以通过设置环境变量来覆盖配置文件。
例如，要覆盖 `frontend_port` 设置，您可以设置 `FRONTEND_PORT` 环境变量。

```bash
FRONTEND_PORT=3001 reflex run
```

## 命令行参数

最后，您可以通过向 `reflex run` 命令传递命令行参数来覆盖配置文件和环境变量。

```bash
reflex run --frontend-port 3001
```

请参阅[CLI参考]({cli_api_ref_url})以获取所有可用的参数。

## 匿名使用统计信息

Reflex 收集关于一般使用情况的完全匿名遥测数据。
参与此匿名计划是可选的，如果您不希望共享任何信息，您可以选择退出。

### 收集的信息

遥测功能允许我们了解 Reflex 的使用情况、最重要的功能以及如何改进产品。

以下信息将被收集：
* 操作系统
* CPU 数量
* 内存
* Python 版本
* Reflex 版本

### 如何退出

要禁用遥测功能，请在您的 `rxconfig.py` 文件中设置 `telemetry_enabled=False`。

```python
config = rx.Config(
    app_name="hello",
    telemetry_enabled=False,
)
```

或者，可以将 `TELEMETRY_ENABLED` 环境变量设置为 `False`。
```

