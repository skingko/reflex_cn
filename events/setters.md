```python
# Setters

每个基本变量都有一个内置的事件处理程序，用于方便地设置其值，称为 `set_VARNAME`。

假设您想要更改选择组件的值。您可以编写自己的事件处理程序来完成此操作：

```python
def handleSelectChange(value):
    # Custom logic to handle value change
    # 自定义逻辑处理值的变化
    pass
```

或者，您可以使用内置的setter以使代码更简洁。

```python
set_selected(value)
```

在此示例中，`selected`的setter是`set_selected`。这两个示例都是等效的。

使用setter是使您的代码更简洁的好方法。但是，如果您想做更复杂的事情，您总是可以在状态中编写自己的函数。
```

