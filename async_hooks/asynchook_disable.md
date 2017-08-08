
* 返回 {AsyncHook} `asyncHook`的参照。

从要执行的AsyncHook回调的全局池中禁用给定“AsyncHook”实例的回调。一旦钩被禁用，直到被启用时才会再次被调用。

为了API的一致性，`disable()`也返回`AsyncHook`实例。

