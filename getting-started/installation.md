```python exec
from pcweb import constants
import reflex as rx
app_name = "my_app_name"
default_url = "http://localhost:3000"
```

# 安装

## 先决条件
Reflex 需要 Python 3.8+。

对于 Windows 用户，我们建议使用 [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/about) 以获得最佳性能。

macOS (Apple Silicon) 用户需要安装 [Rosetta 2](https://support.apple.com/en-us/HT211861)。运行以下命令：
    
`/usr/sbin/softwareupdate --install-rosetta --agree-to-license`

## 虚拟环境

我们**强烈建议**为您的项目创建虚拟环境。

[venv]({constants.VENV_URL}) 是标准选项。[conda]({constants.CONDA_URL}) 和 [poetry]({constants.POETRY_URL}) 是一些替代方案。

## 在 macOS/Linux 上安装
我们将在这里选择 [venv]({constants.VENV_URL})。

### 创建项目目录
将 `{app_name}` 替换为您的项目名称。切换到新目录。
```text
mkdir {app_name}
cd {app_name}
```
### 设置虚拟环境
```text
python3 -m venv .venv
source .venv/bin/activate
```

```md alert warning
# Error `No module named venv`

While Python typically ships with `venv` it is not installed by default on some systems.
If so, please install it manually. E.g. on Ubuntu Linux, run `sudo apt-get install python3-venv`.
```

### 安装 Reflex 包
Reflex 可作为 [pip](constants.PIP_URL) 包使用。
```text
pip install reflex
```

```md alert warning
# Error `command not found: pip`

While Python typically ships with `pip` as the standard package management tool, it is not installed by default on some systems.
You may need to install it manually. E.g. on Ubuntu Linux, run `apt-get install python3-pip`
```

### 初始化项目
```text
reflex init
```

```md alert warning
# Error `command not found: reflex`
If you install Reflex with no virtual environment and get this error it means your `PATH` cannot find the reflex package. 
A virtual environment should solve this problem, or you can try running `python3 -m` before the reflex command.
```

## 在 Windows 上安装

WSL 用户应参考上面 Linux 的说明。

在接下来的部分中，我们将使用本机 Windows (非-WSL)。

我们将在这里选择 [venv]({constants.VENV_URL})，用于虚拟环境。

### 创建新项目目录
```text
mkdir {app_name}
cd {app_name}
```
### 设置虚拟环境
```text
py -3 -m venv .venv
.venv\\Scripts\\activate
```
### 安装 Reflex 包
```text
pip install reflex
```
### 初始化项目
```text
reflex init
```

```md alert warning
# Error `command not found: reflex`

The Reflex framework includes the `reflex` command line (CLI) tool. Using a virtual environment is highly recommended for a seamless experience (see below).",
```

## 运行应用
在开发模式下运行：
```text
reflex run
```
您的应用将在 [http://localhost:3000](http://localhost:3000) 上运行。

Reflex 将日志打印到终端。要增加日志详细程度以帮助调试，请使用 `--loglevel` 标志：
```text
reflex run --loglevel debug
```
Reflex 将在开发模式下实时 *热重新加载* 任何代码更改。您的代码编辑将自动显示在 [http://localhost:3000](http://localhost:3000) 上。

## (可选) 运行演示应用
演示应用展示了 Reflex 的一些特性。
```text
reflex demo
```

