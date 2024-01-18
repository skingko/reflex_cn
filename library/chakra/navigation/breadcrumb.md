---
components:
  - rx.chakra.Breadcrumb
  - rx.chakra.BreadcrumbItem
  - rx.chakra.BreadcrumbLink
---

```python exec
import reflex as rx
```

# 面包屑导航

面包屑导航可以帮助用户在网站中更好地导航到前一页。

对于包含大量页面的网站而言，这非常有用。

```python demo
rx.breadcrumb(
    rx.breadcrumb_item(rx.breadcrumb_link("Home", href="#")),
    rx.breadcrumb_item(rx.breadcrumb_link("Docs", href="#")),
    rx.breadcrumb_item(rx.breadcrumb_link("Breadcrumb", href="#")),
)
```

separator属性可用于更改默认的分隔符。

```python demo
rx.breadcrumb(
    rx.breadcrumb_item(rx.breadcrumb_link("Home", href="#")),
    rx.breadcrumb_item(rx.breadcrumb_link("Docs", href="#")),
    rx.breadcrumb_item(rx.breadcrumb_link("Breadcrumb", href="#")),
    separator=">",
    color="rgb(107,99,246)"
)
```

