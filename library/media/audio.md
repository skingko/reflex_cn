---
components:
    - rx.Audio
---

```python exec
import reflex as rx
```

音频组件可以根据给定的 `src` 路径显示音频。这可以是来自资产文件夹的本地路径，也可以是外部链接。

```python demo
rx.audio(
    url="https://www.learningcontainer.com/wp-content/uploads/2020/02/Kalimba.mp3", 
    width="400px",
    height="auto"
)
```

如果在 `assets` 文件夹中有一个名为 `test.mp3` 的本地文件，我们可以设置 `url="/test.mp3"` 来查看音频文件。

