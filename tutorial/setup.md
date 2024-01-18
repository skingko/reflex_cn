```python exec
from pcweb import constants
import reflex as rx
```

# 设置您的项目

我们将从创建一个新项目并设置好开发环境开始。首先，为您的项目创建一个新目录并切换到该目录。

```bash
~ $ mkdir chatapp
~ $ cd chatapp
```

接下来，我们将为我们的项目创建一个虚拟环境。这是可选的，但建议这样做。在这个例子中，我们将使用 [venv]({constants.VENV_URL}) 来创建我们的虚拟环境。

```bash
chatapp $ python3 -m venv venv
$ source venv/bin/activate
```

现在，我们将安装 Reflex 并创建一个新项目。这将在我们的项目目录中创建一个新的目录结构。

```bash
chatapp $ pip install reflex
chatapp $ reflex init
────────────────────────────────── Initializing chatapp ───────────────────────────────────
Success: Initialized chatapp
chatapp $ ls
assets          chatapp         rxconfig.py     venv
```
```python eval
rx.box(height="20px")
```
您可以运行模板应用程序以确保一切正常。

```bash
chatapp $ reflex run
─────────────────────────────────── Starting Reflex App ───────────────────────────────────
Compiling:  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 1/1 0:00:00
─────────────────────────────────────── App Running ───────────────────────────────────────
App running at: http://localhost:3000
```

```python eval
rx.box(height="20px")
```

您应该看到您的应用程序正在 [http://localhost:3000]({"http://localhost:3000"}) 上运行。

Reflex 还启动了处理所有状态管理和与前端通信的后端服务器。您可以通过访问 [http://localhost:8000/ping]({"http://localhost:8000/ping"}) 来测试后端服务器是否正在运行。

现在，我们已经设置好了项目，在下一节中，我们将开始构建我们的应用程序！

