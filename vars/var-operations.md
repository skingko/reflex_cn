# 变量操作

Var操作可以转换前端中值的占位符表示，并提供了一种在Var上执行基本操作的方式，而无需定义计算的Var。

在前端组件中，不能在状态变量上使用任意的Python函数。例如，以下代码会**不起作用**。

```python
This is because we compile the frontend to Javascript, but the value of `State.number`
is only known at runtime.
```

这是因为我们将前端编译为JavaScript，但`State.number`的值只在运行时可知。

在下面的示例中，我们使用Var操作来连接一个`string`和一个`var`，这意味着我们不需要将其作为计算的Var在状态中执行。

```python
```python demo exec
coins = ["BTC", "ETH", "LTC", "DOGE"]

class VarSelectState(rx.State):
    selected: str = "DOGE"

def var_operations_example():
    return rx.vstack(
        # Using a var operation to concatenate a string with a var.
        rx.heading("I just bought a bunch of " + VarSelectState.selected),
        # Using an f-string to interpolate a var.
        rx.text(f"{VarSelectState.selected} is going to the moon!"),
        rx.select(
            coins,
            value=VarSelectState.selected,
            on_change=VarSelectState.set_selected,
        )
    )
```

```md alert success
# Vars support many common operations.
They can be used for arithmetic, string concatenation, inequalities, indexing, and more. See the [full list of supported operations](/docs/api-reference/var).
```
```

## 支持的操作

Var操作允许我们在前端更改Var，而无需在状态的后端创建更多的计算Var。

一些简单的例子是`==` Var操作符，用于检查两个Var是否相等，以及`to_string()` Var操作符，用于将Var转换为字符串。

```python
```python demo exec

fruits = ["Apple", "Banana", "Orange", "Mango"]

class EqualsState(rx.State):
    selected: str = "Apple"
    favorite: str = "Banana"


def var_equals_example():
    return rx.vstack(
        rx.text(EqualsState.favorite.to_string() + "is my favorite fruit!"),
        rx.select(
            fruits,
            value=EqualsState.selected,
            on_change=EqualsState.set_selected,
        ),
        rx.cond(
            EqualsState.selected == EqualsState.favorite,
            rx.text("The selected fruit is equal to the favorite fruit!"),
            rx.text("The selected fruit is not equal to the favorite fruit."),
        ),
    )

```
```

### 取反，绝对值和长度

减号`-`操作符用于获取Var的负数。绝对值`abs()`操作符用于获取Var的绝对值。`.length()`操作符用于获取列表Var的长度。

```python
```python demo exec
import random

class OperState(rx.State):
    number: int
    numbers_seen: list = []
    def update(self):
        self.number = random.randint(-100, 100)
        self.numbers_seen.append(self.number)

def var_operation_example():
    return rx.vstack(
        rx.heading(f"The number: {OperState.number}", size="md"),
        rx.hstack(
            rx.text("Negated:", rx.badge(-OperState.number, variant="subtle", color_scheme="green")), 
            rx.text(f"Absolute:", rx.badge(abs(OperState.number), variant="subtle", color_scheme="blue")),
            rx.text(f"Numbers seen:", rx.badge(OperState.numbers_seen.length(), variant="subtle", color_scheme="red")),
        ),
        rx.button("Update", on_click=OperState.update),
    )
```
```

### 比较和数学运算符

所有比较运算符在Python中使用的预期方式均可使用。这些包括`==`、`!=`、`>`、`>=`、`<`、`<=`。

有一些运算符可以将两个Var相加`+`，相减`-`，相乘`*`，以及将一个Var的值提升为指数`pow()`。

```python
```python demo exec
import random

class CompState(rx.State):
    number_1: int
    number_2: int

    def update(self):
        self.number_1 = random.randint(-10, 10)
        self.number_2 = random.randint(-10, 10)

def var_comparison_example():
    
    return rx.vstack(
        rx.table_container(
            rx.table(
                headers=["Integer 1", "Integer 2", "Operation", "Outcome"],
                rows=[
                    (CompState.number_1, CompState.number_2, "Int 1 == Int 2", f"{CompState.number_1 == CompState.number_2}"),
                    (CompState.number_1, CompState.number_2, "Int 1 != Int 2", f"{CompState.number_1 != CompState.number_2}"),
                    (CompState.number_1, CompState.number_2, "Int 1 > Int 2", f"{CompState.number_1 > CompState.number_2}"),
                    (CompState.number_1, CompState.number_2, "Int 1 >= Int 2", f"{CompState.number_1 >= CompState.number_2}"),
                    (CompState.number_1, CompState.number_2, "Int 1 < Int 2 ", f"{CompState.number_1 < CompState.number_2}"),
                    (CompState.number_1, CompState.number_2, "Int 1 <= Int 2", f"{CompState.number_1 <= CompState.number_2}"),
                    (CompState.number_1, CompState.number_2, "Int 1 + Int 2", f"{CompState.number_1 + CompState.number_2}"),
                    (CompState.number_1, CompState.number_2, "Int 1 - Int 2", f"{CompState.number_1 - CompState.number_2}"),
                    (CompState.number_1, CompState.number_2, "Int 1 * Int 2", f"{CompState.number_1 * CompState.number_2}"),
                    (CompState.number_1, CompState.number_2, "pow(Int 1, Int2)", f"{pow(CompState.number_1, CompState.number_2)}"),
                ],
                variant="striped",
                color_scheme="teal",
            ),
        ),
        rx.button("Update", on_click=CompState.update),
    )
```
```

### 真除法、底部除法和余数

运算符`/`表示真除法。运算符`//`表示底部除法。运算符`%`表示除法的余数。

```python
```python demo exec
import random

class DivState(rx.State):
    number_1: float = 3.5
    number_2: float = 1.4

    def update(self):
        self.number_1 = round(random.uniform(5.1, 9.9), 2)
        self.number_2 = round(random.uniform(0.1, 4.9), 2)

def var_div_example():
    return rx.vstack(
        rx.table_container(
            rx.table(
                headers=["Integer 1", "Integer 2", "Operation", "Outcome"],
                rows=[
                    (DivState.number_1, DivState.number_2, "Int 1 / Int 2", f"{DivState.number_1 / DivState.number_2}"),
                    (DivState.number_1, DivState.number_2, "Int 1 // Int 2", f"{DivState.number_1 // DivState.number_2}"),
                    (DivState.number_1, DivState.number_2, "Int 1 % Int 2", f"{DivState.number_1 % DivState.number_2}"),
                    ],
                variant="striped",
                color_scheme="red",
            ),
        ),
        rx.button("Update", on_click=DivState.update),
    )
```
```

### 与、或和非

在Reflex中，符号`&`代表逻辑与运算符，表示仅当两个条件同时为真时才返回真。符号`|`代表逻辑或运算符，在前端中使用时，表示当一个或两个条件为真时返回真。符号`~`用于反转Var，仅用于`bool`类型的Var，等效于`not`运算符。

```python
```python demo exec
import random

class LogicState(rx.State):
    var_1: bool = True
    var_2: bool = True

    def update(self):
        self.var_1 = random.choice([True, False])
        self.var_2 = random.choice([True, False])

def var_logical_example():
    return rx.vstack(
        rx.table_container(
            rx.table(
                headers=["Var 1", "Var 2", "Operation", "Outcome"],
                rows=[
                    (f"{LogicState.var_1}", f"{LogicState.var_2}", "Logical AND (&)", f"{LogicState.var_1 & LogicState.var_2}"),
                    (f"{LogicState.var_1}", f"{LogicState.var_2}", "Logical OR (|)", f"{LogicState.var_1 | LogicState.var_2}"),
                    (f"{LogicState.var_1}", f"{LogicState.var_2}", "The invert of Var 1 (~)", f"{~LogicState.var_1}"),
                    ],
                variant="striped",
                color_scheme="green",
            ),
        ),
        rx.button("Update", on_click=LogicState.update),
    )
```
```

### 包含、反转和拼接

不支持Var类型的`in`运算符，我们必须使用`Var.contains()`替代。当我们使用`contains`时，Var必须是类型为`dict`、`list`、`tuple`或`str`的Var。`contains`检查一个Var是否包含我们传递给它的对象作为参数。

我们使用`reverse`操作来反转一个列表Var。Var必须是类型为`list`的Var。

最后，我们使用`join`操作将列表Var拼接成一个字符串。

```python
```python demo exec
class ListsState(rx.State):
    list_1: list = [1, 2, 3, 4, 6]
    list_2: list = [7, 8, 9, 10]
    list_3: list = ["p","y","t","h","o","n"]

def var_list_example():
    return rx.hstack(
        rx.vstack(
            rx.heading(f"List 1: {ListsState.list_1}", size="md"),
            rx.text(f"List 1 Contains 3: {ListsState.list_1.contains(3)}"),
        ),
        rx.vstack(
            rx.heading(f"List 2: {ListsState.list_2}", size="md"),
            rx.text(f"Reverse List 2: {ListsState.list_2.reverse()}"),
        ),
        rx.vstack(
            rx.heading(f"List 3: {ListsState.list_3}", size="md"),
            rx.text(f"List 3 Joins: {ListsState.list_3.join()}"),
        ),
    )
```
```

### 小写、大写和拆分

`lower`操作符将字符串Var转换为小写。`upper`操作符将字符串Var转换为大写。`split`操作符将字符串Var拆分为列表。

```python
```python demo exec
class StringState(rx.State):
    string_1: str = "PYTHON is FUN"
    string_2: str = "react is hard"
   

def var_string_example():
    return rx.hstack(
        rx.vstack(
            rx.heading(f"List 1: {StringState.string_1}", size="md"),
            rx.text(f"List 1 Lower Case: {StringState.string_1.lower()}"),
        ),
        rx.vstack(
            rx.heading(f"List 2: {StringState.string_2}", size="md"),
            rx.text(f"List 2 Upper Case: {StringState.string_2.upper()}"),
            rx.text(f"Split String 2: {StringState.string_2.split()}"),  
        ),
    )
```
```

## 获取项目（索引）

索引仅支持字符串、列表、元组、字典和数据帧。要对一个状态Var进行索引，需要严格的类型注解。

```python
```python
class GetItemState1(rx.State):
    list_1: list = [50, 10, 20]

def get_item_error_1():
    return rx.vstack(
        rx.circular_progress(value=GetItemState1.list_1[0])
    )
```
```

在上面的代码中，您会期望对列表_1状态Var的第一个索引进行索引。实际上，上面的代码会抛出错误：`Invalid var passed for prop value, expected type <class 'int'>, got value of type typing.Any.`这是因为列表中的项的类型在状态中尚未明确定义。要修复这个问题，您需要将列表_1的定义更改为`list_1: list[int] = [50, 10, 20]`。

```python
```python demo exec
class GetItemState1(rx.State):
    list_1: list[int] = [50, 10, 20]

def get_item_error_1():
    return rx.vstack(
        rx.circular_progress(value=GetItemState1.list_1[0])
    )
```
```

### 与Foreach一起使用

在使用索引和`foreach`时经常发生错误。

```python
```python
class ProjectsState(rx.State):
    projects: List[dict] = [
        {
            "technologies": ["Next.js", "Prisma", "Tailwind", "Google Cloud", "Docker", "MySQL"]
        },
        {
            "technologies": ["Python", "Flask", "Google Cloud", "Docker"]
        }
    ]

def get_badge(technology: str) -> rx.Component:
    return rx.badge(technology, variant="subtle", color_scheme="green")

def project_item(project: dict):

    return rx.box(
        rx.hstack(            
            rx.foreach(project["technologies"], get_badge)
        ),
    )
```
```

上面的代码会抛出错误`TypeError: Could not foreach over var of type Any. (If you are trying to foreach over a state var, add a type annotation to the var.)`。

我们必须将`projects: list[dict]`更改为`projects: list[dict[str, list]]`，因为虽然projects已经有注释，但是project["technologies"]中的项目没有注释。

```python
```python demo exec
class ProjectsState(rx.State):
    projects: list[dict[str, list]] = [
        {
            "technologies": ["Next.js", "Prisma", "Tailwind", "Google Cloud", "Docker", "MySQL"]
        },
        {
            "technologies": ["Python", "Flask", "Google Cloud", "Docker"]
        }
    ]


def projects_example() -> rx.Component:
    def get_badge(technology: str) -> rx.Component:
        return rx.badge(technology, variant="subtle", color_scheme="green")

    def project_item(project: dict) -> rx.Component:

        return rx.box(
            rx.hstack(            
                rx.foreach(project["technologies"], get_badge)
            ),
        )
    return rx.box(rx.foreach(ProjectsState.projects, project_item))
```
```

前面的示例中，每个字典的`键`和`值`只有一个类型。对于复杂的多类型数据，您需要使用`Base var`，如下所示。

```python
```python demo exec
class ActressType(rx.Base):
    actress_name: str
    age: int
    pages: list[dict[str, str]]

class MultiDataTypeState(rx.State):
    """The app state."""
    actresses: list[ActressType] = [
        ActressType(
            actress_name="Ariana Grande",
            age=30,
            pages=[
                {"url": "arianagrande.com"}, {"url": "https://es.wikipedia.org/wiki/Ariana_Grande"}
            ]
        ),
        ActressType(
            actress_name="Gal Gadot",
            age=38,
            pages=[
                {"url": "http://www.galgadot.com/"}, {"url": "https://es.wikipedia.org/wiki/Gal_Gadot"}
            ]
        )
    ] 

def actresses_example() -> rx.Component:
    def showpage(page: dict[str, str]):
        return rx.vstack(
            rx.text(page["url"]),
        )

    def showlist(item: ActressType):
        return rx.vstack(
            rx.hstack(
                rx.text(item.actress_name),
                rx.text(item.age),
            ),
            rx.foreach(item.pages, showpage),
        )
    return rx.box(rx.foreach(MultiDataTypeState.actresses, showlist))

```
```

将`actresses`的类型设置为`actresses: list[dict[str,str]]`将失败，因为无法理解`pages key`的`value`实际上是一个`list`。

## 合并多个Var操作

您还可以组合多个Var操作，如下例所示。

```python
```python demo exec
import random

class VarNumberState(rx.State):
    number: int

    def update(self):
        self.number = random.randint(0, 100)

def var_number_example():
    return rx.vstack(
        rx.heading(f"The number is {VarNumberState.number}", size="lg"),
        # Var operations can be composed for more complex expressions.
        rx.cond(
            VarNumberState.number % 2 == 0,
            rx.text("Even", color="green"),
            rx.text("Odd", color="red"),
        ),
        rx.button("Update", on_click=VarNumberState.update),
    )
```
```

我们本可以创建一个返回`number`的奇偶性的计算Var，但是使用Var操作可能更简单。

Var操作可以通常串联以生成复合表达式，但是某些复杂的变换不受Var操作的支持，必须使用计算Var在后端计算值。

