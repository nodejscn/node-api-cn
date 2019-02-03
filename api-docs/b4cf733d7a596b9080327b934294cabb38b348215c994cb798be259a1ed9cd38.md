<!-- YAML
added: v9.7.0
-->

* 返回: {Immediate} 对 `immediate` 的引用。

调用时，只要 `Immediate` 处于活动状态，就会请求 Node.js 事件循环不会退出。 
多次调用 `immediate.ref()` 将无效。

默认情况下，所有 `Immediate` 对象都是 ref 的，通常不需要调用 `immediate.ref()`，除非之前调用了 `immediate.unref()`。

