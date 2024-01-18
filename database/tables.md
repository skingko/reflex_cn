# 表格

表格是包含数据库中所有数据的数据库对象。

在表格中，数据按照行列格式逻辑地组织，类似于电子表格。每一行代表一个唯一的记录，每一列代表记录中的一个字段。

## 创建表格

要创建表格，需要创建一个继承自 `rx.Model` 的类。

以下示例展示了如何创建名为 `User` 的表格。

```python
class User(rx.Model, table=True):
    username: str
    email: str
```

`table=True` 参数告诉 Reflex 在数据库中创建一个表格来存储这个类。

### 主键

默认情况下，Reflex 会为每个表格创建一个名为 `id` 的主键列。

然而，如果一个 `rx.Model` 通过 `primary_key=True` 定义了一个不同的字段，那么默认的 `id` 字段将不会被创建。一个表格也可以重新定义 `id`。

目前无法创建没有主键的表格。

## 高级列类型

SQLModel会自动将基本的Python类型映射为SQLAlchemy列类型，但是对于更高级的使用场景，可以直接使用 `sqlalchemy` 定义列类型。例如，我们可以将一个最后更新的时间戳作为合适的带时区的 `DateTime` 字段添加到帖子示例中。

```python
import datetime

import sqlmodel
import sqlalchemy

class Post(rx.Model, table=True):
    ...
    update_ts: datetime.datetime = sqlmodel.Field(
        default=None,
        sa_column=sqlalchemy.Column(
            "update_ts",
            sqlalchemy.DateTime(timezone=True),
            server_default=sqlalchemy.func.now(),
        ),
    )
```

为了使 `Post` 模型在前端更易用，可以提供一个 `dict` 方法将任何字段转换为可JSON序列化的值。在这种情况下，dict 方法覆盖了默认的 `datetime` 序列化器，去掉了微秒部分。

```python
class Post(rx.Model, table=True):
    ...

    def dict(self, *args, **kwargs) -> dict:
        d = super().dict(*args, **kwargs)
        d["update_ts"] = self.update_ts.replace(microsecond=0).isoformat()
        return d
```

