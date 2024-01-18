# 数据库

Reflex使用[sqlmodel](https://sqlmodel.tiangolo.com)来提供内置的ORM包装SQLAlchemy。

本页面的示例是针对Reflex如何使用各种工具来提供集成的数据库接口。下面只包括了基本用例，但您可以参考[sqlmodel教程](https://sqlmodel.tiangolo.com/tutorial/select/)了解更多示例和信息，只需将`SQLModel`替换为`rx.Model`，将`Session(engine)`替换为`rx.session()`。

对于高级用例，请参阅[SQLAlchemy文档](https://docs.sqlalchemy.org/en/14/orm/quickstart.html)（v1.4）。

## 连接

Reflex提供内置的SQLite数据库用于存储和检索数据。

您可以通过修改`rxconfig.py`文件中的数据库URL来连接到自己的SQL兼容数据库。

```python
config = rx.Config(
    app_name="my_app",
    db_url="sqlite:///reflex.db",
)
```

有关可用的数据库URL示例，请参阅[SQLAlchemy文档](https://docs.sqlalchemy.org/en/14/core/engines.html#backend-specific-urls)。请确保安装适用于您打算使用的数据库的适当的DBAPI驱动程序。

## 表格

要创建一个表格，可以创建一个继承自`rx.Model`的类，并指定它是一个表格。

```python
class User(rx.Model, table=True):
    username: str
    email: str
    password: str   
```

## 迁移

Reflex利用[alembic](https://alembic.sqlalchemy.org/en/latest/)来管理数据库模式更改。

在新应用程序中使用数据库功能之前，必须调用`reflex db init`来初始化alembic并创建具有当前模式的迁移脚本。

在对模式进行更改后，使用`reflex db makemigrations --message 'something changed'`生成一个位于`alembic/versions`目录中的脚本，该脚本将更新数据库模式。建议在应用脚本之前进行检查。

使用`reflex db migrate`命令将迁移脚本应用于将数据库更新到最新状态。在应用程序启动期间，如果Reflex检测到当前的数据库模式不是最新的，将在控制台上显示警告信息。

## 查询

要查询数据库，可以创建一个`rx.session()`来处理打开和关闭数据库连接。

您可以使用常规的SQLAlchemy查询来查询数据库。

```python
with rx.session() as session:
    session.add(User(username="test", email="admin@pynecone.io", password="admin"))
    session.commit()
```

