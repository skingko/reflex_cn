# Reflex Hosting Service

```python exec
import reflex as rx
from pcweb import constants
from pcweb.pages import docs
from pcweb.templates.docpage import doccmdoutput
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
```

到目前为止，我们一直在我们自己的机器上本地运行我们的应用程序。
但是，如果我们想与世界分享我们的应用程序呢？这就是托管服务的用途。

```md alert info
Hosting is in Alpha. Please reach out to us on Discord if you are ready to deploy and we will give you an invitation code.
```

## 快速开始

Reflex的托管服务让您无需担心配置基础设施就可以轻松部署您的应用程序。

### 先决条件

1. 托管服务需要 `reflex>=0.3.2`。
2. 本教程假设您已经成功将您的应用程序初始化并运行了 `reflex init` 和 `reflex run` 命令。
3. 还请确保您的顶级应用程序目录中有一个 `requirements.txt` 文件，其中包含了您的所有Python依赖项！

### 身份验证

首先，请使用以下命令创建一个帐户或登录。

```bash
reflex login
```

您将被重定向到您的浏览器，您可以通过GitHub或Gmail进行身份验证。

### 部署

成功验证后，您可以开始部署您的应用程序。

导航至要部署的项目目录，并键入以下命令：

```bash
reflex deploy
```

默认情况下，该命令是交互式的。它会询问您一些问题以获取部署所需的信息。

**名称**：为部署的应用程序选择一个名称。这个名称将成为部署应用程序的URL的一部分，即 `<app-name>.reflex.run`。名称应仅包含域名安全字符：无斜杠，无下划线。域名不区分大小写。为避免混淆，您在此选择的名称也不区分大小写。如果您输入大写字母，我们会自动将它们转换为小写字母。

**地区**：在此输入地区代码，或按 `Enter` 键接受默认值。默认代码 `sjc` 代表美国西海岸的加利福尼亚州圣何塞市。请查看支持的地区列表：[Reflex部署地区](#reflex-deployments-regions)。

**环境变量**：`环境变量` 是指环境变量。您在应用程序中可能根本没有使用过它们。在这种情况下，按 `Enter` 键跳过。关于环境变量的更多信息，请参阅后面的部分 [环境变量](#environment-variables)。

就是这些！您应该会收到有关部署进度的一些反馈，几分钟后，您的应用程序应该就会运行起来。🎉

```md alert info
Once your code is uploaded, the hosting service will start the deployment. After a complete upload, exiting from the command **does not** affect the deployment process. The command prints a message when you can safely close it without affecting the deployment.
```

## 在操作中观看

下面是将 [AI chat app]({docs.tutorial.intro.path}) 部署到我们的托管服务的视频。

```python eval
rx.center(
    rx.video(url="https://www.youtube.com/embed/pf3FKE26hx4"),
    rx.box(height="3em"),
    width="100%",
    padding_y="2em"
)
```

