# 命令行界面（CLI）

`reflex` 命令行界面（CLI）是用于创建和管理 Reflex 应用的工具。

要查看所有可用命令的列表，请运行 `reflex --help`。

```bash
$ reflex --help

Usage: reflex [OPTIONS] COMMAND [ARGS]...

  Reflex CLI to create, run, and deploy apps.

Options:
  -v, --version  Get the Reflex version.
  --help         Show this message and exit.

Commands:
  db           Subcommands for managing the database schema.
  demo         Run the demo app.
  deploy       Deploy the app to the Reflex hosting service.
  deployments  Subcommands for managing the Deployments.
  export       Export the app to a zip file.
  init         Initialize a new Reflex app in the current directory.
  login        Authenticate with Reflex hosting service.
  logout       Log out of access to Reflex hosting service.
  run          Run the app in the current directory.
```

## 初始化

`reflex init` 命令在当前目录下创建一个新的 Reflex 应用。
如果已经存在 `rxconfig.py` 文件，它将使用最新的模板重新初始化应用。

```bash
$ reflex init --help
Usage: reflex init [OPTIONS]

  Initialize a new Reflex app in the current directory.

Options:
  --name APP_NAME                 The name of the app to initialize.
  --template [demo|sidebar|blank]
                                  The template to initialize the app with.
  --loglevel [debug|info|warning|error|critical]
                                  The log level to use.  [default:
                                  LogLevel.INFO]
  --help                          Show this message and exit.
```

## 运行

`reflex run` 命令在当前目录中运行应用程序。

默认情况下，它以开发模式运行您的应用程序。
这意味着当您对代码进行更改时，应用程序将自动重新加载。
您还可以以生产模式运行，它将创建一个经过优化的应用程序构建。

您可以通过标志配置模式和其他选项。

```bash
$ reflex run --help
Usage: reflex run [OPTIONS]

  Run the app in the current directory.

Options:
  --env [dev|prod]                The environment to run the app in.
                                  [default: Env.DEV]
  --frontend-only                 Execute only frontend.
  --backend-only                  Execute only backend.
  --frontend-port TEXT            Specify a different frontend port.
                                  [default: 3000]
  --backend-port TEXT             Specify a different backend port.  [default:
                                  8000]
  --backend-host TEXT             Specify the backend host.  [default:
                                  0.0.0.0]
  --loglevel [debug|info|warning|error|critical]
                                  The log level to use.  [default:
                                  LogLevel.INFO]
  --help                          Show this message and exit.
```

## 导出

您可以使用 `reflex export` 命令将应用程序的前端和后端导出为 zip 文件。

前端是一个编译后的 NextJS 应用程序，可以部署到像 Github Pages 或 Vercel 这样的静态托管服务。
但是这只是一个静态构建，您需要单独部署后端。
有关更多信息，请参阅自托管指南。

