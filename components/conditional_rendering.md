# 条件渲染

我们使用 `cond` 组件来进行条件性渲染。`cond` 组件的使用方式类似于 Python 中的条件（三元）运算符，类似于 `if-else` 语句。

以下是一个简单的示例，展示了通过检查状态变量 `show` 的值来渲染蓝色文本或红色文本的方法。

`cond` 组件的第一个参数是我们要检查的条件。这里的条件是状态变量布尔型 `show` 的值。

如果 `show` 为 `True`，则会渲染 `cond` 组件的第二个参数，本例中为 `rx.text("Text 1", color="blue")`。

如果 `show` 为 `False`，则会渲染 `cond` 组件的第三个参数，本例中为 `rx.text("Text 2", color="red")`。

## 变量操作（否定）

您可以使用 `cond` 组件进行变量操作。要了解更多关于变量操作符的信息，请查看[这些文档]({vars.var_operations.path})。逻辑运算符 `~` 可以用来对条件取反。在这个例子中，我们展示了通过否定 `~CondNegativeState.show` 条件后，在 `cond` 内部渲染 `rx.text("Text 1", color="blue")` 组件时，当状态变量 `show` 为负时。

## 多个条件

还可以使用逻辑或（|）和逻辑与（&）运算符来组合复杂的条件。

这里我们使用了变量操作符 `>=`、`<=`、`&` 的例子。我们定义了一个条件，如果一个人的年龄在 18 到 65 岁之间（包括这些年龄），则可以工作，否则不能工作。

我们也可以使用运算符 `|` 代表一个条件中的 `逻辑或`。

## 重复使用 Cond

我们还可以通过在返回一个 `cond` 的函数中定义它来多次重复使用 `cond` 组件。

在这个例子中，我们定义了函数 `render_item`。这个函数接收一个 `item`，使用 `cond` 来检查 `item` 是否 `is_packed`。如果已打包，则返回带有 `✔` 的 `item_name`，否则只返回 `item_name`。

## 嵌套条件

我们还可以嵌套 `cond` 组件以创建更复杂的逻辑。在 Python 中，我们可以有一个 `if` 语句，然后有几个 `elif` 语句，最后以 `else` 结束。在 Reflex 中，使用嵌套的 `cond` 组件也是可能的。在这个例子中，我们检查一个数是正数、负数还是零。

以下是使用 `if` 语句的 Python 逻辑：

```python
```python
number = 0

if number > 0:
    print("Positive number")

elif number == 0:
    print('Zero')
else:
    print('Negative number')
```
```

以下是逻辑相同的 Reflex 代码：

```python
```python demo exec
import random


class NestedState(rx.State):
    
    num: int = 0

    def change(self):
        self.num = random.randint(-10, 10)


def cond_nested_example():
    return rx.vstack(
        rx.button("Toggle", on_click=NestedState.change),
        rx.cond(
            NestedState.num > 0,
            rx.text(f"{NestedState.num} is Positive!", color="orange"),
            rx.cond(
                NestedState.num == 0,
                rx.text(f"{NestedState.num} is Zero!", color="blue"),
                rx.text(f"{NestedState.num} is Negative!", color="red"),
            )
        ),
    )

```
```

这是一个更高级的例子，我们有三个数字，并且正在检查其中哪个是最大的。如果其中任意两个相等，则返回 `Some of the numbers are equal!`。

以下 Reflex 代码在逻辑上等同于在 Python 中执行以下操作：

```python
```python
a = 8
b = 10
c = 2

if((a>b and a>c) and (a != b and a != c)): 
	print(a, " is the largest!") 
elif((b>a and b>c) and (b != a and b != c)): 
	print(b, " is the largest!") 
elif((c>a and c>b) and (c != a and c != b)): 
	print(c, " is the largest!") 
else: 
	print("Some of the numbers are equal!") 
```
```

## Cond 作为样式属性

`cond` 也可以用于在 Reflex 应用中显示和隐藏内容。在这个例子中，`cond` 运算符的第三个参数为空，这意味着如果条件为假，则不会渲染任何内容。

```python demo exec
class CondStyleState(rx.State):
    show: bool = False
    img_url: str = "/preview.png"
    def change(self):
        self.show = not (self.show)


def cond_style_example():
    return rx.vstack(
        rx.button("Toggle", on_click=CondStyleState.change),
        rx.cond(
            CondStyleState.show,
            rx.image(
                src=CondStyleState.img_url,
                height="25em",
                width="25em",
            ),
        ),
    )
```

