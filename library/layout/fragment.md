---

components:
    - rx.Fragment
---

```python exec
import reflex as rx
from pcweb import constants
```

Fragment 是一个组件，它允许你将多个组件分组，而无需使用包裹节点。

有关其用法的更多信息，请参阅 React 文档中的 [React/Fragment]({constants.FRAGMENT_COMPONENT_INFO_URL})。

```python demo
rx.fragment(
    rx.text("Component1"), 
    rx.text("Component2")
)
```

