
<!-- YAML
added: v8.1.0
-->

* `callbacks` {Object} 注册的回调
* 返回: 用于禁用和启用钩的`{AsyncHook}`实例

注册要为每个异步操作的不同生命周期事件调用的函数。

在资源生命周期中，对相应的异步事件调用`init()`/`before()`/`after()`/`destroy()`回调。

所有的回调都是可选的。因此，例如，如果只需要跟踪资源清理，那么只需要传递`destroy`回调。 可以传递给`callbacks`的所有函数的细节可以查看[`Hook Callbacks`] []。

