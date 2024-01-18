# 关系

外键关系用于链接两个表。例如，`Post`模型可以有一个字段`user_id`，它的外键是`user.id`，指向一个`User`模型。这样我们就可以自动查询与用户关联的`Post`对象，或者找到与`Post`关联的`User`对象。

要建立双向关系，模型必须在_relationship_中正确设置`back_populates`关键字参数，以指向_other_模型中的相关属性。

## 外键关系

要创建关系，首先在模型中添加一个字段，引用相关表的主键，然后添加一个`sqlmodel.Relationship`属性，用于访问相关对象。

以示例中的`sqlmodel`对象为例，定义这样的关系需要使用。

```python
from typing import List, Optional

import sqlmodel

import reflex as rx


class Post(rx.Model, table=True):
    title: str
    body: str
    user_id: int = sqlmodel.Field(foreign_key="user.id")

    user: Optional["User"] = sqlmodel.Relationship(back_populates="posts")
    flags: Optional[List["Flag"]] = sqlmodel.Relationship(back_populates="post")


class User(rx.Model, table=True):
    username: str
    email: str

    posts: List[Post] = sqlmodel.Relationship(back_populates="user")
    flags: List["Flag"] = sqlmodel.Relationship(back_populates="user")


class Flag(rx.Model, table=True):
    post_id: int = sqlmodel.Field(foreign_key="post.id")
    user_id: int = sqlmodel.Field(foreign_key="user.id")
    message: str

    post: Optional[Post] = sqlmodel.Relationship(back_populates="flags")
    user: Optional[User] = sqlmodel.Relationship(back_populates="flags")
```

更多详情请参阅[SQLModel关系文档](https://sqlmodel.tiangolo.com/tutorial/relationship-attributes/define-relationships-attributes/)。

## 查询关系

### 插入关联对象

以下示例假定标记用户存储在状态中作为一个`User`实例，并且帖子`id`提供在在表单中提交的数据中。

```python
class FlagPostForm(rx.State):
    user: User

    def flag_post(self, form_data: dict[str, str]):
        with rx.session() as session:
            post = session.get(Post, int(form_data.pop("post_id")))
            flag = Flag(message=form_data.pop("message"), post=post, user=self.user)
            session.add(flag)
            session.commit()
```

### 如何取消关联？

默认情况下，关系属性是**惰性加载**或者"select"模式，即在访问关系属性时生成一个查询。惰性加载通常适用于单个对象的查找和操作，但是在访问多个关联对象进行序列化时可能效率较低。

有几种可用的替代加载机制可以设置在关系对象上或者在执行查询时设置。

* "joined" 或 `joinload` - 生成一个单一查询以一次性加载所有相关对象。
* "subquery" 或 `subqueryload` - 生成一个单一查询以一次性加载所有相关对象，但使用子查询来进行连接，而不是在主查询中进行连接。
* "selectin" 或 `selectinload` - 发出第二个（或更多）SELECT语句，将父对象的主键标识符组装到一个IN子句中，以便通过主键一次性加载所有相关集合/标量引用的成员。

还有一些非加载机制，"raise" 和 "noload"，用于明确避免加载关系。

每种加载方法都有权衡，适用于不同的数据访问模式。
更多详情，请参阅[SQLAlchemy：关系加载技术](https://docs.sqlalchemy.org/en/14/orm/loading_relationships.html)。

### 查询关联对象

要查询`Post`表并包括所有的`User`和`Flag`对象，可以使用`.options`接口来指定所需关系的`selectinload`。使用这种方法，关联的对象将在前端代码中可用于渲染，而无需额外的步骤。

```python
import sqlalchemy


class PostState(rx.State):
    posts: List[Post]

    def load_posts(self):
        with rx.session() as session:
            self.posts = session.exec(
                Post.select
                .options(
                    sqlalchemy.orm.selectinload(Post.user),
                    sqlalchemy.orm.selectinload(Post.flags).options(
                        sqlalchemy.orm.selectinload(Flag.user),
                    ),
                )
                .limit(15)
            ).all()
```

加载方法会创建新的查询对象，因此如果关系本身具有需要加载的其他关系，则可以链接。在这个示例中，由于`Flag`引用了`User`，所以`Flag.user`关系必须从`Post.flags`关系中进行链式加载。

### 在关系上指定加载机制

或者，可以在关系上通过将`sa_relationship_kwargs=\{"lazy": method}`传递给`sqlmodel.Relationship`来指定加载机制，默认情况下在所有查询中使用给定的加载机制。

```python
from typing import List, Optional

import sqlmodel

import reflex as rx


class Post(rx.Model, table=True):
    ...
    user: Optional["User"] = sqlmodel.Relationship(
        back_populates="posts",
        sa_relationship_kwargs=\{"lazy": "selectin"},
    )
    flags: Optional[List["Flag"]] = sqlmodel.Relationship(
        back_populates="post",
        sa_relationship_kwargs=\{"lazy": "selectin"},
    )
```

