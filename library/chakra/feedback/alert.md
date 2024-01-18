---
components:
    - rx.chakra.Alert
    - rx.chakra.AlertIcon
    - rx.chakra.AlertTitle
    - rx.chakra.AlertDescription
---

```python exec
import reflex as rx
```

# 警告

警告用于传达影响系统、功能或页面的状态。下面是不同警告状态的示例。

```python demo
rx.vstack(
    rx.alert(
        rx.alert_icon(),
        rx.alert_title("Error Reflex version is out of date."),
        status="error",
    ),
    rx.alert(
        rx.alert_icon(),
        rx.alert_title("Warning Reflex version is out of date."),
        status="warning",
    ),
    rx.alert(
        rx.alert_icon(),
        rx.alert_title("Reflex version is up to date."),
        status="success",
    ),
    rx.alert(
        rx.alert_icon(),
        rx.alert_title("Reflex version is 0.1.32."),
        status="info",
    ),
    width="100%",
)
```

除了不同的状态类型，警告还可以有不同的样式变种和可选的描述。默认情况下，变种为“subtle”。

```python demo
rx.vstack(
    rx.alert(
        rx.alert_icon(),
        rx.alert_title("Reflex version is up to date."),
        rx.alert_description("No need to update."),
        status="success",
        variant="subtle",
    ),
    rx.alert(
        rx.alert_icon(),
        rx.alert_title("Reflex version is up to date."),
        status="success",
        variant="solid",
    ),
    rx.alert(
        rx.alert_icon(),
        rx.alert_title("Reflex version is up to date."),
        status="success",
        variant="top-accent",
    ),
    width="100%",
)
```

