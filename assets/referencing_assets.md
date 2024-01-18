```markdown
```python exec
import reflex as rx
```

# 资源

静态文件（例如图片和样式表）可以放在项目的 "assets/" 文件夹中。这些文件可以在应用程序中引用。

## 引用资源

要引用 "assets/" 中的图片，只需将相对路径作为属性传递。

例如，您可以将标识放在您的资产文件夹中：
```bash
assets
└── Reflex.svg
```

然后，您可以使用 `rx.image` 组件来显示它：

```python demo
rx.image(src="/Reflex.svg", width="5em")
```

## 网站图标

网站图标是显示在浏览器选项卡中的小图标。

您可以将 "favicon.ico" 文件添加到 "assets/" 文件夹中以更改网站图标。
```

