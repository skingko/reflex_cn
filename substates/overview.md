```python exec
import reflex as rx
```

# 子状态

子状态可以将您的状态分解为多个类，使其更易于管理。这对于应用程序的增长非常有用，因为它允许您将每个页面视为独立的实体。子状态还允许您共享公共的状态资源，例如变量或事件处理程序。

## 多个状态

一个常见的模式是为应用程序中的每个页面创建子状态。
这使您可以将每个页面视为独立的实体，并且随着应用程序的增长，更易于管理代码。

要创建子状态，只需多次继承`rx.State`：

```python
# index.py
import reflex as rx

class IndexState(rx.State):
    """Define your main state here."""
    data: str = "Hello World"


@rx.page()
def index():
    return rx.box(rx.text(IndexState.data)

# signup.py
import reflex as rx


class SignupState(rx.State):
    """Define your signup state here."""
    username: str = ""
    password: str = ""

    def signup(self):
        ...


@rx.page()
def signup_page():
    return rx.box(
        rx.input(value=SignupState.username),
        rx.input(value=SignupState.password),
    )

# login.py
import reflex as rx

class LoginState(rx.State):
    """Define your login state here."""
    username: str = ""
    password: str = ""

    def login(self):
        ...

@rx.page()
def login_page():
    return rx.box(
        rx.input(value=LoginState.username),
        rx.input(value=LoginState.password),
    )
```

分开状态只是一种组织方式。您仍然可以通过导入状态类来从其他页面访问状态。

```python
# index.py

import reflex as rx

from signup import SignupState

...

def index():
    return rx.box(
        rx.text(IndexState.data),
        rx.input(value=SignupState.username),
        rx.input(value=SignupState.password),
    )
```

## 状态继承

子状态还可以继承自`rx.State`之外的另一个子状态，从而创建一个状态层次结构。

例如，您可以创建一个基本状态来定义在应用程序的所有页面中都常见的变量和事件处理程序，例如当前登录的用户。

```python
class BaseState(rx.State):
    """Define your base state here."""

    current_user: str = ""

    def logout(self):
        self.current_user = ""


class LoginState(BaseState):
    """Define your login state here."""

    username: str = ""
    password: str = ""

    def login(self, username, password):
        # authenticate
        authenticate(...)

        # Set the var on the parent state. 
        self.current_user = username
```

您可以从子子状态访问父状态属性，但无法从父状态访问子状态的属性。

