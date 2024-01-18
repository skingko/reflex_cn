```javascript
# 浏览器Javascript

Reflex将作为Python函数定义的前端代码编译成运行在用户浏览器中的Javascript Web应用程序。有些情况下，您可能需要提供自定义的Javascript代码来与Web API进行交互，使用某些第三方库，或者封装不通过Reflex的Python API暴露的底层功能。

## 执行脚本

在Reflex应用程序中执行自定义Javascript代码有四种方式：

* `rx.script` - 通过`next/script`注入脚本以实现内联和外部Javascript代码的高效加载。详细信息请参阅[组件库](/docs/library/other/script/)中的说明。
  * 这些组件可以直接包含在页面的主体中，或者可以通过`rx.App(head_components=[rx.script(...)])`传递到`<Head>`标签中以包含到所有页面中。
* `rx.call_script` - 一个事件处理程序，用于评估任意Javascript代码，并可选择将结果返回给另一个事件处理程序。

前两种方法可以结合使用，以加载外部脚本，然后在用户事件响应中调用其中定义的函数。

以下两种方法专门用于封装组件，并在[Wrapping React]({wrapping_react.overview.path})部分中使用示例进行描述。

* 在`rx.Component`子类中使用`_get_hooks`和`_get_custom_code`
* 使用`Var.create`和`_var_is_local=False`

## 内联脚本

推荐使用`rx.script`组件加载内联Javascript以获得对前端行为的更大控制。

可以通过`rx.call_script`接口从后端事件处理程序或前端事件触发器访问脚本中的函数和变量。

## 外部脚本

外部脚本可以从`assets`目录或CDN URL中加载，然后通过`rx.call_script`进行控制。

## 访问客户端值

`rx.call_script`函数接受一个期望接收评估Javascript代码结果的事件处理程序，该处理程序带有一个参数。可以使用这个参数访问客户端的值，例如`window.location`或当前滚动位置，或任何先前定义的值。

## 使用React Hooks

要在Reflex应用程序中直接使用React Hooks，必须对`rx.Component`进行子类化，通常使用`rx.Fragment`来处理没有可见元素的钩子功能。钩子代码由`_get_hooks`方法返回，该方法应返回包含插入到页面组件（即渲染函数本身）中的Javascript代码的`str`。

对于必须在组件渲染函数之外定义的支持代码，请使用`_get_custom_code`。

以下示例使用`useEffect`在`document`对象上注册全局热键，并在按下特定按键时触发事件。
```

