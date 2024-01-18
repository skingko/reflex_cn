```python exec
import reflex as rx
from typing import Any
```
# 复杂例子

在这个更复杂的例子中，我们将会封装 `reactflow` 这个用于构建基于节点的应用程序，比如流程图、图表、图形等的库。

## 导入

让我们从导入库 [reactflow](https://www.npmjs.com/package/reactflow) 开始。让我们创建一个名为 `reactflow.py` 的独立文件，并添加以下代码：

```python 
from reflex.components.component import Component
from typing import Any, Dict, List, Union
from reflex.vars import Var

class ReactFlowLib(Component):
    """A component that wraps a react flow lib."""

    library = "reactflow"

    def _get_custom_code(self) -> str:
        return """import 'reactflow/dist/style.css';
        """
```

注意，我们还使用了 `_get_custom_code` 方法来导入所需的用于样式的 css 文件。

## 组件

在本教程中，我们将封装 Reactflow 的三个组件：`ReactFlow`、`Background` 和 `Controls`。让我们从 `ReactFlow` 组件开始。

在这里，我们将定义需要使用该组件的 `tag` 和 `vars`。

我们还将定义 `get_event_triggers` 方法来指定组件触发的事件。在本教程中，我们将使用 `on_edges_change` 和 `on_connect`，但你可以在 [reactflow 文档](https://reactflow.dev/docs/api/react-flow-props/#onnodeschange) 中找到组件触发的所有事件。

```python
from reflex.components.component import Component
from typing import Any, Dict, List, Union
from reflex.vars import Var

class ReactFlowLib(Component):
    ...

class ReactFlow(ReactFlowLib):

    tag = "ReactFlow"

    nodes: Var[List[Dict[str, Any]]]

    edges: Var[List[Dict[str, Any]]]

    fit_view: Var[bool]

    nodes_draggable: Var[bool]

    nodes_connectable: Var[bool]

    nodes_focusable: Var[bool]

    def get_event_triggers(self) -> dict[str, Any]:
        return {
            **super().get_event_triggers(),
            "on_edges_change": lambda e0: [e0],
            "on_connect": lambda e0: [e0],
        }
```

现在，让我们添加 `Background` 和 `Controls` 组件。我们还将使用 `create` 方法来创建这些组件，以便在我们的应用程序中使用它们。

```python
from reflex.components.component import Component
from typing import Any, Dict, List, Union
from reflex.vars import Var

class ReactFlowLib(Component):
    ...

class ReactFlow(ReactFlowLib):
    ...

class Background(ReactFlowLib):

    tag = "Background"

    color: Var[str]

    gap: Var[int]

    size: Var[int]

    variant: Var[str]

class Controls(ReactFlowLib):

    tag = "Controls"

react_flow = ReactFlow.create
background = Background.create
controls = Controls.create
```

## 构建应用程序

现在我们有了组件，让我们来构建应用程序。

首先，让我们定义我们应用程序中将要使用的初始节点和边缘。

```python
import reflex as rx
from .react_flow import react_flow, background, controls
import random
from typing import Any, Dict, List


initial_nodes = [
    \{
        'id': '1',
        'type': 'input',
        'data': \{'label': '150'},
        'position': \{'x': 250, 'y': 25},
    },
    \{
        'id': '2',
        'data': \{'label': '25'},
        'position': \{'x': 100, 'y': 125},
    },
    \{
        'id': '3',
        'type': 'output',
        'data': \{'label': '5'},
        'position': \{'x': 250, 'y': 250},
    },
]

initial_edges = [
    \{'id': 'e1-2', 'source': '1', 'target': '2', 'label': '*', 'animated': True},
    \{'id': 'e2-3', 'source': '2', 'target': '3', 'label': '+', 'animated': True},
]
```

接下来，我们将定义应用程序的状态。我们有三个事件处理程序：`add_random_node`、`clear_graph` 和 `on_edges_change`。

`on_edges_change` 事件处理程序将在边缘发生改变时被调用。在这种情况下，我们将使用它来删除已存在的边缘，并添加新的边缘。它接收一个名为 `new_edge` 的参数，该参数是一个包含边缘的 `source` 和 `target` 的字典。

```python
class State(rx.State):
    """The app state."""
    nodes: List[Dict[str, Any]] = initial_nodes
    edges: List[Dict[str, Any]] = initial_edges
    
    def add_random_node(self):
        new_node_id = f'\{len(self.nodes) + 1\}'
        node_type = random.choice(['default'])
        # Label is random number
        label = new_node_id
        x = random.randint(0, 500)
        y = random.randint(0, 500)

        new_node = {
            'id': new_node_id,
            'type': node_type,
            'data': \{'label': label},
            'position': \{'x': x, 'y': y},
            'draggable': True,
        }
        self.nodes.append(new_node)

    def clear_graph(self):
        self.nodes = []  # Clear the nodes list
        self.edges = []  # Clear the edges list

    def on_edges_change(self, new_edge):
        # Iterate over the existing edges
        for i, edge in enumerate(self.edges):
            # If we find an edge with the same ID as the new edge
            if edge["id"] == f"e\{new_edge['source']}-\{new_edge['target']}":
                # Delete the existing edge
                del self.edges[i]
                break

        # Add the new edge
        self.edges.append({
            "id": f"e\{new_edge['source']}-\{new_edge['target']}",
            "source": new_edge["source"],
            "target": new_edge["target"],
            "label": random.choice(["+", "-", "*", "/"]),
            "animated": True,
        })
```

现在让我们定义应用程序的用户界面。我们将使用 `react_flow` 组件，并从我们的状态中传递 `nodes` 和 `edges`。我们还将为 `react_flow` 组件添加 `on_connect` 事件处理程序，以处理连接边缘的情况。

```python
def index() -> rx.Component:
    return rx.vstack(
        react_flow(
            background(),
            controls(),
            nodes_draggable=True,
            nodes_connectable=True,
            on_connect=lambda e0: State.on_edges_change(e0),
            nodes=State.nodes,
            edges=State.edges,
            fit_view=True,
        ),
        rx.hstack(
            rx.button("Clear graph", on_click=State.clear_graph, width="100%"),
            rx.button("Add node", on_click=State.add_random_node, width="100%"),
            width="100%",
        ),
        height="30em",
        width="100%",
    )


# Add state and page to the app.
app = rx.App()
app.add_page(index)
```

```python exec
import reflex as rx
from reflex.components.component import Component
from typing import Any, Dict, List, Union
from reflex.vars import Var
import random

class ReactFlowLib(Component):
    """A component that wraps a react flow lib."""

    library = "reactflow"

    def _get_custom_code(self) -> str:
        return """import 'reactflow/dist/style.css';
        """

class ReactFlow(ReactFlowLib):

    tag = "ReactFlow"

    nodes: Var[List[Dict[str, Any]]]

    edges: Var[List[Dict[str, Any]]]

    fit_view: Var[bool]

    nodes_draggable: Var[bool]

    nodes_connectable: Var[bool]

    nodes_focusable: Var[bool]

    def get_event_triggers(self) -> dict[str, Any]:
        return {
            **super().get_event_triggers(),
            "on_edges_change": lambda e0: [e0],
            "on_connect": lambda e0: [e0],
        }


class Background(ReactFlowLib):

    tag = "Background"

    color: Var[str]

    gap: Var[int]

    size: Var[int]

    variant: Var[str]

class Controls(ReactFlowLib):

    tag = "Controls"

react_flow = ReactFlow.create
background = Background.create
controls = Controls.create

initial_nodes = [
    {
        'id': '1',
        'type': 'input',
        'data': {'label': '150'},
        'position': {'x': 250, 'y': 25},
    },
    {
        'id': '2',
        'data': {'label': '25'},
        'position': {'x': 100, 'y': 125},
    },
    {
        'id': '3',
        'type': 'output',
        'data': {'label': '5'},
        'position': {'x': 250, 'y': 250},
    },
]

initial_edges = [
    {'id': 'e1-2', 'source': '1', 'target': '2', 'label': '*', 'animated': True},
    {'id': 'e2-3', 'source': '2', 'target': '3', 'label': '+', 'animated': True},
]


class ReactFlowState(rx.State):
    """The app state."""
    nodes: List[Dict[str, Any]] = initial_nodes
    edges: List[Dict[str, Any]] = initial_edges
    
    def add_random_node(self):
        new_node_id = f'{len(self.nodes) + 1}'
        node_type = random.choice(['default'])
        # Label is random number
        label = new_node_id
        x = random.randint(0, 250)
        y = random.randint(0, 250)

        new_node = {
            'id': new_node_id,
            'type': node_type,
            'data': {'label': label},
            'position': {'x': x, 'y': y},
            'draggable': True,
        }
        print(new_node)
        self.nodes.append(new_node)

    def clear_graph(self):
        self.nodes = []  # Clear the nodes list
        self.edges = []  # Clear the edges list

    def on_edges_change(self, new_edge):
        # Iterate over the existing edges
        for i, edge in enumerate(self.edges):
            # If we find an edge with the same ID as the new edge
            if edge["id"] == f"e{new_edge['source']}-{new_edge['target']}":
                # Delete the existing edge
                del self.edges[i]
                break

        # Add the new edge
        self.edges.append({
            "id": f"e{new_edge['source']}-{new_edge['target']}",
            "source": new_edge["source"],
            "target": new_edge["target"],
            "label": random.choice(["+", "-", "*", "/"]),
            "animated": True,
        })
```

这是应用程序运行的示例：

```python eval
rx.vstack(
        react_flow(
            background(),
            controls(),
            nodes_draggable=True,
            nodes_connectable=True,
            on_connect=lambda e0: ReactFlowState.on_edges_change(e0),
            nodes=ReactFlowState.nodes,
            edges=ReactFlowState.edges,
            fit_view=True,
        ),
        rx.hstack(
            rx.button("Clear graph", on_click=ReactFlowState.clear_graph, width="100%"),
            rx.button("Add node", on_click=ReactFlowState.add_random_node, width="100%"),
            width="100%",
        ),
        height="30em",
        width="100%",
    )
```

