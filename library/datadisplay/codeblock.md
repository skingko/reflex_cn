---
components:
    - rx.CodeBlock
---

```python exec
import reflex as rx
```

# 代码块

CodeBlock 组件可以轻松地在网站中显示代码。
输入多行字符串并指定语言以显示所需的代码。

```python demo
rx.code_block(
    """def fib(n):
    if n <= 1:
        return n
    else:
        return(fib(n-1) + fib(n-2))""",
    language="python",
    show_line_numbers=True,
)
```

