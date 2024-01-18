```yaml
组件：
  - rx.Script
```

```python exec
import reflex as rx
```

# 脚本

Script组件可用于通过URL包含内联JavaScript或JavaScript文件。

它使用[`next/script`组件](https://nextjs.org/docs/app/api-reference/components/script)来注入脚本，并且可以安全地与条件渲染一起使用，以便通过状态来控制脚本副作用。

```python
rx.script("console.log('inline javascript')")
```

应避免复杂的内联脚本。
如果要包含的代码超过几行，更可维护的做法是在`assets`目录中实现一个单独的JavaScript文件，并通过`src`属性来包含它。

```python
rx.script(src="/my-custom.js")
```

该组件特别适用于包含跟踪和社交脚本。
可以通过`custom_attrs`属性提供所需的脚本标签的任何附加属性。

```python
rx.script(src="//gc.zgo.at/count.js", custom_attrs=\{"data-goatcounter": "https://reflextoys.goatcounter.com/count"})
```

以下代码可渲染为以下内容，以便通过第三方服务进行统计计数。

```html
<script src="//gc.zgo.at/count.js" data-goatcounter="https://reflextoys.goatcounter.com/count" data-nscript="afterInteractive"></script>
```

