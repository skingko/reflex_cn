---
components:
    - rx.radix.themes.ScrollArea
---


```python exec
import random
import reflex as rx
from reflex.components.radix.themes.components import *
from reflex.components.radix.themes.layout import *
from reflex.components.radix.themes.typography import *
from pcweb.templates.docpage import style_grid
```



# 滚动区域

使用原生功能定制样式的跨浏览器可滚动区域。

## 基本示例

```python demo
scroll_area(
    flex(
        text(
            """Three fundamental aspects of typography are legibility, readability, and
        aesthetics. Although in a non-technical sense “legible” and “readable”
        are often used synonymously, typographically they are separate but
        related concepts.""",
            as_="p",
        ),
        text(
            """Legibility describes how easily individual characters can be
        distinguished from one another. It is described by Walter Tracy as “the
        quality of being decipherable and recognisable”. For instance, if a “b”
        and an “h”, or a “3” and an “8”, are difficult to distinguish at small
        sizes, this is a problem of legibility.""",
            as_="p",
        ),
        text(
            """Typographers are concerned with legibility insofar as it is their job to
        select the correct font to use. Brush Script is an example of a font
        containing many characters that might be difficult to distinguish. The
        selection of cases influences the legibility of typography because using
        only uppercase letters (all-caps) reduces legibility.""",
            as_="p",
        ),
        direction="column",
        gap="4",
    ),
    type="always",
    scrollbars="vertical",
    style={"height": 180},

)

```


## 控制可滚动轴

使用 `scrollbars` 属性来限制可滚动的轴。该属性可以取值 `"vertical" | "horizontal" | "both"`。


```python demo
grid(
    scroll_area(
        flex(
            text(
                """Three fundamental aspects of typography are legibility, readability, and
        aesthetics. Although in a non-technical sense "legible" and "readable"
        are often used synonymously, typographically they are separate but
        related concepts.""",
                size="2", trim="both",
            ),
            text(
                """Legibility describes how easily individual characters can be
        distinguished from one another. It is described by Walter Tracy as "the
        quality of being decipherable and recognisable". For instance, if a "b"
        and an "h", or a "3" and an "8", are difficult to distinguish at small
        sizes, this is a problem of legibility.""",
                size="2", trim="both",
            ),
            p="2", pr="8", direction="column", gap="4",
        ),
        type_="always",
        scrollbars="vertical",
        style={"height": 150}, 
    ),
    scroll_area(
        flex(
            text(
                """Three fundamental aspects of typography are legibility, readability, and
        aesthetics. Although in a non-technical sense "legible" and "readable"
        are often used synonymously, typographically they are separate but
        related concepts.""",
                size="2", trim="both",
            ),
            text(
                """Legibility describes how easily individual characters can be
        distinguished from one another. It is described by Walter Tracy as "the
        quality of being decipherable and recognisable". For instance, if a "b"
        and an "h", or a "3" and an "8", are difficult to distinguish at small
        sizes, this is a problem of legibility.""",
                size="2", trim="both",
            ),
            p="2", gap="4", style={"width": 700},
        ),
        type_="always",
        scrollbars="horizontal",
        style={"height": 150}, 
    ),
    scroll_area(
        flex(
            text(
                """Three fundamental aspects of typography are legibility, readability, and
        aesthetics. Although in a non-technical sense "legible" and "readable"
        are often used synonymously, typographically they are separate but
        related concepts.""",
                size="2", trim="both",
            ),
            text(
                """Legibility describes how easily individual characters can be
        distinguished from one another. It is described by Walter Tracy as "the
        quality of being decipherable and recognisable". For instance, if a "b"
        and an "h", or a "3" and an "8", are difficult to distinguish at small
        sizes, this is a problem of legibility.""",
                size="2", trim="both",
            ),
            p="2", gap="4", style={"width": 400},
        ),
        type_="always",
        scrollbars="both",
        style={"height": 150}, 
    ),
    columns="3",
    gap="2",
)
```


## 设置滚动条类型

`type_` 属性描述了滚动条可见性的特性。

`auto` 表示当内容在相应方向上溢出时，滚动条可见。

`always` 表示不管内容是否溢出，滚动条始终可见。

`scroll` 表示当用户沿着相应方向滚动时滚动条可见。

`hover` 表示当用户沿着相应方向滚动时以及鼠标悬停在滚动区域上时滚动条可见。


```python demo
grid(
    scroll_area(
        flex(
            text("type_= 'auto'",  weight="bold"),
            text(
                """Legibility describes how easily individual characters can be
        distinguished from one another. It is described by Walter Tracy as "the
        quality of being decipherable and recognisable". For instance, if a "b"
        and an "h", or a "3" and an "8", are difficult to distinguish at small
        sizes, this is a problem of legibility.""",
                size="2", trim="both",
            ),
            p="2", direction="column", gap="4",
        ),
        type_="auto",
        scrollbars="vertical",
        style={"height": 150}, 
    ),
    scroll_area(
        flex(
            text("type_= 'always'",  weight="bold"),
            text(
                """Legibility describes how easily individual characters can be
        distinguished from one another. It is described by Walter Tracy as "the
        quality of being decipherable and recognisable". For instance, if a "b"
        and an "h", or a "3" and an "8", are difficult to distinguish at small
        sizes, this is a problem of legibility.""",
                size="2", trim="both",
            ),
            p="2", direction="column", gap="4",
        ),
        type_="always",
        scrollbars="vertical",
        style={"height": 150}, 
    ),
    scroll_area(
        flex(
            text("type_= 'scroll'",  weight="bold"),
            text(
                """Legibility describes how easily individual characters can be
        distinguished from one another. It is described by Walter Tracy as "the
        quality of being decipherable and recognisable". For instance, if a "b"
        and an "h", or a "3" and an "8", are difficult to distinguish at small
        sizes, this is a problem of legibility.""",
                size="2", trim="both",
            ),
            p="2", direction="column", gap="4",
        ),
        type_="scroll",
        scrollbars="vertical",
        style={"height": 150}, 
    ),
    scroll_area(
        flex(
            text("type_= 'hover'",  weight="bold"),
            text(
                """Legibility describes how easily individual characters can be
        distinguished from one another. It is described by Walter Tracy as "the
        quality of being decipherable and recognisable". For instance, if a "b"
        and an "h", or a "3" and an "8", are difficult to distinguish at small
        sizes, this is a problem of legibility.""",
                size="2", trim="both",
            ),
            p="2", direction="column", gap="4",
        ),
        type_="hover",
        scrollbars="vertical",
        style={"height": 150}, 
    ),
    columns="4",
    gap="2",
)

```


## 样式


### 大小

### 圆角





