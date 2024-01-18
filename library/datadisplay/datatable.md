---

components:
    - rx.DataTable
---

```python exec
import reflex as rx
```

# DataTable（数据表）

数据表组件是以表格形式展示数据的绝佳方式。您可以通过将 Pandas dataframe 传递给 `data` 属性来创建表格。

在此示例中，我们将从 CSV 文件中读取数据，将其转换为 Pandas dataframe，并在数据表中显示出来。

我们还将为数据表添加搜索、分页和排序功能，以提高其可访问性。


```python demo box
rx.data_table(
    data=[
        ["Avery Bradley", "6-2", 25.0],
        ["Jae Crowder", "6-6", 25.0],
        ["John Holland", "6-5", 27.0],
        ["R.J. Hunter", "6-5", 22.0],
        ["Jonas Jerebko", "6-10", 29.0],
        ["Amir Johnson", "6-9", 29.0],
        ["Jordan Mickey", "6-8", 21.0],
        ["Kelly Olynyk", "7-0", 25.0],
        ["Terry Rozier", "6-2", 22.0],
        ["Marcus Smart", "6-4", 22.0],
    ],
    columns=["Name", "Height", "Age"],
    pagination=True,
    search=True,
    sort=True,
)
```

```python
import pandas as pd
nba_data = pd.read_csv("https://media.geeksforgeeks.org/wp-content/uploads/nba.csv")"""
...
rx.data_table(
    data = nba_data[["Name", "Height", "Age"]],
    pagination= True,
    search= True,
    sort= True,
)  
```

下面的示例展示了如何从列表创建数据表。

```python
class State(rx.State):
    data: List = [
        ["Lionel", "Messi", "PSG"],
        ["Christiano", "Ronaldo", "Al-Nasir"]
     ]
    columns: List[str] = ["First Name", "Last Name"]
    
def index():  
    return rx.data_table(
        data=State.data,
        columns=State.columns,
    )   
```

