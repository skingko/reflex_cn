# 项目结构

## 目录结构

```python exec
app_name = "hello"
```

让我们创建一个名为 `{app_name}` 的新应用

```bash
mkdir {app_name}
cd {app_name}
reflex init
```

这将创建一个像这样的目录结构:

```bash
{app_name}
├── .web
├── assets
├── {app_name}
│   ├── __init__.py
│   └── {app_name}.py
└── rxconfig.py
```

让我们来看看这些目录和文件的含义。

## .web

这里是存放编译后的 JavaScript 文件的地方。您通常不需要访问此目录，但它可以用于调试。

每个 Reflex 页面都会编译成一个对应的 `.js` 文件，存放在 `.web/pages` 目录中。

## 资源

`assets` 目录是您可以存放任何想公开使用的静态资源的地方。这包括图片、字体和其他文件。

例如，如果您将一张图片保存到 `assets/image.png` 中，您可以在应用中以以下方式显示它:

```python
rx.image(src="image.png")
```

## 主要项目

初始化项目将创建一个与应用同名的目录。这是您编写应用逻辑的地方。

Reflex会在 `{app_name}/{app_name}.py` 文件中生成一个默认的应用程序。您可以修改该文件来定制您的应用程序。

## 配置

`rxconfig.py` 文件用于配置您的应用程序。默认情况下，它的内容如下:

```python
import reflex as rx


config = rx.Config(
    app_name="{app_name}",
)
```

我们将在下一节详细讨论配置。

