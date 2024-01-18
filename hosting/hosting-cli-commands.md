# Reflex Hosting Service CLI Commands（Reflex 托管服务 CLI 命令）

```python exec
import reflex as rx
from pcweb import constants
from pcweb.templates.docpage import doccmdoutput
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
```

## Concepts（概念）

### Requirements（要求）

为了能够部署您的应用程序，我们要求您准备一个包含所有所需 Python 包的 `requirements.txt` 文件。托管服务会根据此文件运行 `pip install` 命令，以准备运行您的应用程序的实例。我们建议您在启动新应用程序时使用 Python 虚拟环境，并仅安装必要的包。这样可以减少准备时间，并仅安装所需的包，从而使您的应用程序部署更快。关于 Python 虚拟环境工具和如何将包捕获到 `requirements.txt` 文件中，网上有很多资源可供参考。

### Environment Variables（环境变量）

在部署到 Reflex 的托管服务时，命令提示符会询问您是否要添加任何环境变量。这些环境变量会被加密并安全存储。我们建议将后端 API 密钥或密码作为 `envs` 输入。请确保输入 `envs` 时不要使用任何引号。

环境变量是键值对。我们不会在任何 CLI 命令中显示它们的值，只显示它们的名称（或键）。然而，如果您的应用程序有意打印这些变量的值，返回的日志仍然包含打印出的值。目前，日志没有对类似秘密的内容进行审查。只有应用程序所有者和 Reflex 团队管理员才能访问这些日志。

您可以通过在应用程序的后端中使用 `os.environ` 引用它们的名称作为键来访问 `envs` 的值。例如，如果您设置了一个 env `ASYNC_DB_URL`，则可以通过 `os.environ["ASYNC_DB_URL"]` 访问它。一些 Python 库会自动查找特定的环境变量，例如，`openai` 的 Python 客户端会查找 `OPENAI_API_KEY`。`boto3` 客户端凭据可以通过设置 `AWS_ACCESS_KEY_ID` 和 `AWS_SECRET_ACCESS_KEY` 来配置。这些信息通常在您使用的 Python 包的文档中可以找到。

### Updating Deployment（更新部署）

要重新部署或更新您的应用程序，请进入项目目录并再次输入 `reflex deploy`。此命令将与托管服务通信，并自动检测具有相同名称的现有应用程序。这次部署命令将覆盖该应用程序。您应该看到类似于 `Overwrite deployment [ app-name ] ...` 的提示。此操作是完全覆盖，不是增量更新。

## CLI Command Reference（CLI 命令参考）

所有的 `reflex` 命令都带有帮助手册。帮助手册列出了可能有用的其他命令选项。您可以输入 `--help` 查看帮助手册。有一些命令是组织在一个 `subcommands` 系列下的。以下是一个示例。请注意，帮助手册的外观可能因 `reflex` 版本或 `reflex-hosting-cli` 版本而异。

```python eval
doccmdoutput(
    command="reflex deployments --help",
    output="""Usage: reflex deployments [OPTIONS] COMMAND [ARGS]...

  Subcommands for managing the Deployments.

Options:
  --help  Show this message and exit.

Commands:
  build-logs  Get the build logs for a deployment.
  delete      Delete a hosted instance.
  list        List all the hosted deployments of the authenticated user.
  logs        Get the logs for a deployment.
  regions     List all the regions of the hosting service.
  status      Check the status of a deployment.
"""
)
```

### Authentication Commands（身份验证命令）

#### reflex login

当您首次输入 `reflex login` 命令时，它会在浏览器中打开托管服务登录页面。我们通过 OAuth 对用户进行身份验证。目前支持的 OAuth 提供程序是 Github 和 Gmail。您应该能够在 Github 和 Google 账户设置页面上撤销此类授权。我们不会登录您的 Github 或 Gmail 账户。OAuth 授权提供了您的电子邮件地址，在 Github 的情况下还提供了用户名。我们使用这些信息为您创建一个帐户。在原始帐户创建中使用的电子邮件用于标识您作为用户。如果您使用不同的电子邮件进行身份验证，则会创建不同的帐户。要切换到另一个帐户，请首先使用 `reflex logout` 命令注销。有关注销命令的更多详细信息，请参阅 [reflex logout](#reflex-logout) 部分。

```python eval
doccmdoutput(
    command="reflex login",
    output="""Opening https://control-plane.reflex.run ...
Successfully logged in.
""",
)
```

认证成功后，浏览器将重定向到原始的托管服务登录页面，并显示您已登录的信息。现在您可以返回到输入登录命令的终端。它应该打印出类似于 `成功登录` 的消息。

您的访问令牌会缓存在 reflex 支持目录中。对于后续的登录命令，会先验证缓存的令牌是否有效。如果令牌仍然有效，CLI 命令只会显示 `您已经登录`。如果令牌已过期或无效，登录命令会尝试再次打开您的浏览器进行基于 Web 的身份验证。

#### reflex logout

当您成功通过托管服务进行身份验证时，有两个不同的地方缓存了信息：在 reflex 支持目录中包含访问令牌的文件，以及浏览器中的 cookies。这些 cookies 包含访问令牌、刷新令牌以及一些表示访问令牌过期的 Unix 时间戳。注销命令会从这些位置删除已缓存的信息。

### Deployment Commands（部署命令）

#### reflex deploy

这是从应用程序的顶级目录部署 Reflex 应用程序的命令。此目录包含一个 `rxconfig.py`，您在其中运行 `reflex init` 和 `reflex run`。

需要一个 `requirements.txt` 文件。部署命令会将此文件的内容与当前 Python 环境中的顶级包进行检查。如果命令检测到您的 Python 环境中有新的包或更新版本的同一包，它会打印出差异并询问您是否希望更新 `requirements.txt`。请务必仔细检查建议的更新内容。此功能是在较新版本的托管 CLI 包 `reflex-hosting-cli>=0.1.3` 中添加的。

```python eval
doccmdoutput(
    command="reflex deploy",
    output="""Info: The requirements.txt may need to be updated.
--- requirements.txt
+++ new_requirements.txt
@@ -1,3 +1,3 @@
-reflex>=0.2.0
-openai==0.28
+openai==0.28.0
+reflex==0.3.8

Would you like to update requirements.txt based on the changes above? [y/n]: y

Choose a name for your deployed app (https://<picked-name>.reflex.run)
Enter to use default. (webui-gray-sun): demo-chat
Region to deploy to. See regions: https://bit.ly/46Qr3mF
Enter to use default. (sjc): lax
Environment variables for your production App ...
 * env-1 name (enter to skip): OPENAI_API_KEY
   env-1 value: sk-*********************
 * env-2 name (enter to skip):
Finished adding envs.
──────────────── Compiling production app and preparing for export. ────────────────
Zipping Backend: ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 12/12 0:00:00
Uploading Backend code and sending request ...
Backend deployment will start shortly.
──────────────── Compiling production app and preparing for export. ────────────────
Compiling: ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 9/9 0:00:00
Creating Production Build:  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 9/9 0:00:07
Zipping Frontend: ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 20/20 0:00:00
Uploading Frontend code and sending request ...
Frontend deployment will start shortly.
───────────────────────────── Deploying production app. ────────────────────────────
Deployment will start shortly: https://demo-chat.reflex.run
Closing this command now will not affect your deployment.
Waiting for server to report progress ...
2024-01-12 12:24:54.188271 PST | Updating frontend...
2024-01-12 12:24:55.074264 PST | Frontend updated!
2024-01-12 12:24:55.137679 PST | Deploy success (frontend)
2024-01-12 12:24:59.722384 PST | Updating backend...
2024-01-12 12:25:01.006386 PST | Building backend image...
2024-01-12 12:26:03.672379 PST | Deploying backend image...
2024-01-12 12:26:21.017946 PST | Backend updated!
2024-01-12 12:26:21.018003 PST | Deploy success (backend)
Waiting for the new deployment to come up
Your site [ demo-chat ] at ['lax'] is up: https://demo-chat.reflex.run
""",
)
```

部署命令默认为交互式。要进行无需交互的部署，请添加 `--no-interactive` 并根据部署设置设置相关命令选项。输入 `reflex deploy --help` 查看有关每个选项的说明的帮助手册。无论部署命令是否交互式，部署顺序都是相同的。

```bash
reflex deploy --no-interactive -k todo -r sjc -r sea --env OPENAI_API_KEY=YOU-KEY-NO-EXTRA-QUOTES --env DB_URL=YOUR-EXTERNAL-DB-URI --env KEY3=THATS-ALOTOF-KEYS
```

#### reflex deployments list

列出所有您的部署。

```python eval
doccmdoutput(
    command="reflex deployments list",
    output="""key                           regions  app_name              reflex_version       cpus     memory_mb  url                                         envs
----------------------------  -------  --------------------  ----------------  -------   -----------  ------------------------------------------  ---------
webui-navy-star               ['sjc']  webui                 0.3.7                   1          1024  https://webui-navy-star.reflex.run          ['OPENAI_API_KEY']
chatroom-teal-ocean           ['ewr']  chatroom              0.3.2                   1          1024  https://chatroom-teal-ocean.reflex.run      []
sales-navy-moon               ['phx']  sales                 0.3.4                   1          1024  https://sales-navy-moon.reflex.run          []
simple-background-tasks       ['yul']  lorem_stream          0.3.7                   1          1024  https://simple-background-tasks.reflex.run  []
snakegame                     ['sjc']  snakegame             0.3.3                   1          1024  https://snakegame.reflex.run                []
basic-crud-navy-apple         ['dfw']  basic_crud            0.3.8                   1          1024  https://basic-crud-navy-apple.reflex.run    []
""",
)
```

#### reflex deployments status `app-name`

获取特定应用程序的状态，包括后端和前端。

```python eval
doccmdoutput(
    command="reflex deployments status clock-gray-piano",
    output="""Getting status for [ clock-gray-piano ] ...

backend_url                                reachable    updated_at
-----------------------------------------  -----------  ------------
https://rxh-prod-clock-gray-piano.fly.dev  False        N/A


frontend_url                               reachable    updated_at
-----------------------------------------  -----------  -----------------------
https://clock-gray-piano.reflex.run        True         2023-10-13 15:23:07 PDT
""",
)
```

#### reflex deployments logs `app-name`

获取特定部署的日志。

返回的日志是在控制台上打印的消息。如果您的代码中有 `print` 语句，它们会显示在这些日志中。默认情况下，日志命令返回最新的 100 行日志，并继续流式传输任何新行。

我们为此命令添加了更多选项，包括 `from` 和 `to` 时间戳以及要获取的日志行数限制。接受的时间戳格式包括 ISO 8601 格式、Unix 时间戳和相对时间戳。相对时间戳是指从 `now` 开始的一段时间之前。单位是 `d（天），h（小时），m（分钟），s（秒）`。例如，`--from 3d --to 4h` 查询从 3 天前到 4 小时前的日志。关于您使用的 CLI 版本中的确切语法，请参考帮助手册。

```python eval
doccmdoutput(
    command="reflex deployments logs todo",
    output="""Note: there is a few seconds delay for logs to be available.
2023-10-13 22:18:39.696028 | rxh-dev-todo | info | Pulling container image registry.fly.io/rxh-dev-todo:depot-1697235471
2023-10-13 22:18:41.462929 | rxh-dev-todo | info | Pulling container image registry.fly.io/rxh-dev-todo@sha256:60b7b531e99e037f2fb496b3e05893ee28f93a454ee618bda89a531a547c4002
2023-10-13 22:18:45.963840 | rxh-dev-todo | info | Successfully prepared image registry.fly.io/rxh-dev-todo@sha256:60b7b531e99e037f2fb496b3e05893ee28f93a454ee618bda89a531a547c4002 (4.500906837s)
2023-10-13 22:18:46.134860 | rxh-dev-todo | info | Successfully prepared image registry.fly.io/rxh-dev-todo:depot-1697235471 (6.438815793s)
2023-10-13 22:18:46.210583 | rxh-dev-todo | info | Configuring firecracker
2023-10-13 22:18:46.434645 | rxh-dev-todo | info | [    0.042971] Spectre V2 : WARNING: Unprivileged eBPF is enabled with eIBRS on, data leaks possible via Spectre v2 BHB attacks!
2023-10-13 22:18:46.477693 | rxh-dev-todo | info | [    0.054250] PCI: Fatal: No config space access function found
2023-10-13 22:18:46.664016 | rxh-dev-todo | info | Configuring firecracker
""",
)
```

#### reflex deployments build-logs `app-name`

获取托管服务部署应用程序的日志。

```python eval
doccmdoutput(
    command="reflex deployments build-logs webcam-demo",
    output="""Note: there is a few seconds delay for logs to be available.
2024-01-08 11:02:46.109785 PST | fly-controller-prod | #8 extracting sha256:bd9ddc54bea929a22b334e73e026d4136e5b73f5cc29942896c72e4ece69b13d 0.0s done | None | None
2024-01-08 11:02:46.109811 PST | fly-controller-prod | #8 DONE 5.3s | None | None
2024-01-08 11:02:46.109834 PST | fly-controller-prod |  | None | None
2024-01-08 11:02:46.109859 PST | fly-controller-prod | #8 [1/4] FROM public.ecr.aws/p3v4g4o2/reflex-hosting-base:v0.1.8-py3.11@sha256:9e8569507f349d78d41a86e1eb29a15ebc9dece487816875bbc874f69dcf7ecf | None | None
...
...
2024-01-08 11:02:50.913748 PST | fly-controller-prod | #11 [4/4] RUN . /home/reflexuser/venv/bin/activate && pip install --no-color --no-cache-dir -q -r /home/reflexuser/app/requirements.txt reflex==0.3.4 | None | None
...
...
2024-01-08 11:03:07.430922 PST | fly-controller-prod | #12 pushing layer sha256:d9212ef47485c9f363f105a05657936394354038a5ae5ce03c6025f7f8d2d425 3.5s done | None | None
2024-01-08 11:03:07.881471 PST | fly-controller-prod | #12 pushing layer sha256:ee46d14ae1959b0cacda828e5c4c1debe32c9c4c5139fb670cde66975a70c019 3.9s done | None | None
...
2024-01-08 11:03:13.943166 PST | fly-controller-prod | Built backend image | None | None
2024-01-08 11:03:13.943174 PST | fly-controller-prod | Deploying backend image... | None | None
2024-01-08 11:03:13.943311 PST | fly-controller-prod | Running sys_run | None | None
...
2024-01-08 11:03:31.005887 PST | fly-controller-prod | Checking for valid image digest to be deployed to machines... | None | None
2024-01-08 11:03:31.005893 PST | fly-controller-prod | Running sys_run | None | None
2024-01-08 11:03:32.411762 PST | fly-controller-prod | Backend updated! | None | None
2024-01-08 11:03:32.481276 PST | fly-controller-prod | Deploy success (backend) | None | None
""",
)
```

在准备和部署应用程序时，托管服务会打印日志消息。这些日志消息称为构建日志。构建日志可用于故障排除部署失败的情况。例如，如果在 `requirements.txt` 中有一个名为 `numpz==1.26.3` 的包（应为 `numpy`），托管服务将无法安装它。该包不存在。我们期望在构建日志中找到几行指示 `pip install` 命令失败的日志。

#### reflex deployments delete `app-name`

删除特定部署。

### Public Commands（公共命令）

这些命令不需要身份验证。

#### reflex deployments regions

列出所有可用于选择部署的有效区域。

```python eval
table_root(
    table_header(
        table_row(
            table_column_header_cell("Region Code"),
            table_column_header_cell("Region"),
        ),
    ),
    table_body(
        table_row(
            table_row_header_cell("alt"),
            table_cell("Atlanta, Georgia (US)"),
        ),
        table_row(
            table_row_header_cell("bog"),
            table_cell("Bogotá, Colombia"),
        ),
        table_row(
            table_row_header_cell("bos"),
            table_cell("Boston, Massachusetts (US)"),
        ),
        table_row(
            table_row_header_cell("cdg"),
            table_cell("Paris, France"),
        ),
        table_row(
            table_row_header_cell("den"),
            table_cell("Denver, Colorado (US)"),
        ),
        table_row(
            table_row_header_cell("dfw"),
            table_cell("Dallas, Texas (US)"),
        ),
        table_row(
            table_row_header_cell("eze"),
            table_cell("Ezeiza, Argentina"),
        ),
        table_row(
            table_row_header_cell("fra"),
            table_cell("Frankfurt, Germany"),
        ),
        table_row(
            table_row_header_cell("hkg"),
            table_cell("Hong Kong, Hong Kong"),
        ),
        table_row(
            table_row_header_cell("iad"),
            table_cell("Ashburn, Virginia (US)"),
        ),
        table_row(
            table_row_header_cell("lax"),
            table_cell("Los Angeles, California (US)"),
        ),
        table_row(
            table_row_header_cell("lhr"),
            table_cell("London, United Kingdom"),
        ),
        table_row(
            table_row_header_cell("mad"),
            table_cell("Madrid, Spain"),
        ),
        table_row(
            table_row_header_cell("mia"),
            table_cell("Miami, Florida (US)"),
        ),
        table_row(
            table_row_header_cell("ord"),
            table_cell("Chicago, Illinois (US)"),
        ),
        table_row(
            table_row_header_cell("scl"),
            table_cell("Santiago, Chile"),
        ),
        table_row(
            table_row_header_cell("sea"),
            table_cell("Seattle, Washington (US)"),
        ),
        table_row(
            table_row_header_cell("sin"),
            table_cell("Singapore, Singapore"),
        ),
        table_row(
            table_row_header_cell("sjc"),
            table_cell("San Jose, California (US)"),
        ),
        table_row(
            table_row_header_cell("syd"),
            table_cell("Sydney, Australia"),
        ),
        table_row(
            table_row_header_cell("waw"),
            table_cell("Warsaw, Poland"),
        ),
        table_row(
            table_row_header_cell("yul"),
            table_cell("Montréal, Canada"),
        ),
        table_row(
            table_row_header_cell("yyz"),
            table_cell("Toronto, Canada"),
        ),
    ),
    variant="surface",
)
```

