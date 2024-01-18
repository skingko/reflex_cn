# 查询

查询用于从数据库中检索数据。

查询是对数据库表或组合表的信息请求。可以使用查询从单个表或多个表中检索数据。查询还可以用于向表中插入、更新或删除数据。

## 会话

要执行查询，首先必须创建一个`rx.session`。您可以使用会话使用SQLModel或SQLAlchemy语法查询数据库。

当代码块执行完成时，`rx.session`语句将自动关闭会话。**如果未调用`session.commit()`，更改将被回滚并且不会持久保存到数据库。**代码还可以通过`session.rollback()`显式回滚而不关闭会话。

以下示例显示了如何创建会话和查询数据库。首先，我们创建一个名为`User`的表。

```python
class User(rx.Model, table=True):
    username: str
    email: str
```

### 选择

然后，我们创建一个会话并查询用户表。

```python
class QueryUser(rx.State):
    name: str
    users: list[User]

    def get_users(self):
        with rx.session() as session:
            self.users = session.exec(User.select.where(User.username.contains(self.name)).all()
```

`get_users`方法将根据状态变量`name`的值查询数据库中包含该值的所有用户。

在较旧版本的Python中，模型对象上的`.select`属性不起作用，但可以使用`sqlmodel.select(User)`代替。

### 插入

类似地，使用`session.add()`方法向数据库添加新记录或保存现有对象。

```python
class AddUser(rx.State):
    username: str
    email: str
    
    def add_user(self):
        with rx.session() as session:
            session.add(User(username=self.username, email=self.email))
            session.commit()
```

### 更新

要更新用户，首先查询数据库以获取对象，进行所需的修改，`.add`对象到会话中，最后调用`.commit()`。

```python
class ChangeEmail(rx.State):
    username: str
    email: str

    def modify_user(self):
        with rx.session() as session:
            user = session.exec(User.select.where((User.username == self.username).first()
            user.email = self.email
            session.add(user)
            session.commit()
```

### 删除

要删除用户，首先查询数据库以获取对象，然后在会话上调用`.delete()`，最后调用`.commit()`。

```python
class RemoveUser(rx.State):
    username: str

    def delete_user(self):
        with rx.session() as session:
            user = session.exec(User.select.where(User.username == self.username).first()
            session.delete(user)
            session.commit()
```

## ORM对象生命周期

查询返回的对象与创建它们的会话绑定，通常不可在该会话之外使用。在添加或更新对象后，并不会自动更新所有字段，因此访问某些属性可能会触发其他查询以刷新对象。

为了避免这种情况，可以使用`session.refresh()`方法显式更新对象，并确保所有字段在退出会话之前都是最新的。

```python
class AddUserForm(rx.State):
    user: User | None = None
    
    def add_user(self, form_data: dict[str, str]):
        with rx.session() as session:
            self.user = User(**form_data)
            session.add(self.user)
            session.commit()
            session.refresh(self.user)
```

现在，`self.user`对象将正确引用自动生成的主键`id`，即使在创建对象时没有提供该键。

如果`self.user`需要在新会话中被修改或用于另一个查询中，则必须将其添加到会话中。将对象添加到会话中并不一定会创建对象，而是将其与可能根据需要创建或更新的会话相关联。

```python
class AddUserForm(rx.State):
    ...
    
    def update_user(self, form_data: dict[str, str]):
        if self.user is None:
            return
        with rx.session() as session:
            self.user.set(**form_data)
            session.add(self.user)
            session.commit()
            session.refresh(self.user)
```

如果要在会话之外引用和访问ORM对象，则应调用`.refresh()`来避免过时对象的异常。

## 直接使用SQL

避免使用SQL是使用ORM的主要优势之一，但有时候在特别复杂的查询或使用特定于数据库的功能时是必要的。

SQLModel提供了`session.execute()`方法，可用于执行原始的SQL字符串。如果需要参数绑定，可以将查询包装在[`sqlalchemy.text`](https://docs.sqlalchemy.org/en/14/core/sqlelement.html#sqlalchemy.sql.expression.text)中，该函数允许使用冒号前缀的名称作为占位符。

```md alert
Never use string formatting to construct SQL queries, as this may lead to SQL injection vulnerabilities in the app.
```

```python
import sqlalchemy

import reflex as rx


class State(rx.State):
    def insert_user_raw(self, username, email):
        with rx.session() as session:
            session.execute(
                sqlalchemy.text(
                    "INSERT INTO user (username, email) "
                    "VALUES (:username, :email)"
                ),
                \{"username": username, "email": email},
            )
            session.commit()

    @rx.var
    def raw_user_tuples(self) -> list[list]:
        with rx.session() as session:
            return [list(row) for row in session.execute("SELECT * FROM user").all()]
```

