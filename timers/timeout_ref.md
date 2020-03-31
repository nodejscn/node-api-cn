<!-- YAML
added: v0.9.1
-->

* 返回: {Timeout} `timeout` 的引用。

当被调用时，则只要 `Timeout` 处于活动状态，就会要求 Node.js 事件循环不要退出。 
多次调用 `timeout.ref()` 没有影响。

默认情况下，所有的 `Timeout` 对象都是 ref 的，通常不需要调用 `timeout.ref()`，除非之前调用了 `timeout.unref()`。


