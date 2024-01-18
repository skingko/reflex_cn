---
components:
    - rx.Video
---

```python exec
import reflex as rx
```

视频组件可以根据传入的src路径显示视频。这可以是来自资产文件夹的本地路径，也可以是外部链接。

```python demo
rx.video(
    url="https://www.youtube.com/embed/9bZkp7q19f0", 
    width="400px",
    height="auto"
)
```

如果我们在`assets`文件夹中有一个名为`test.mp4`的本地文件，我们可以设置`url="/test.mp3"`来查看视频。

