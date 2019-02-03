<!-- YAML
added: v0.9.1
-->

* 返回: {Timeout} 对 `timeout` 的引用。

调用时，只要 `Timeout` 处于活动状态，就会请求 Node.js 事件循环不会退出。 
多次调用 `timeout.ref()` 将无效。

默认情况下，所有 `Timeout` 对象都是 ref 的，通常不需要调用 `timeout.ref()`，除非之前调用了 `timeout.unref()`。

