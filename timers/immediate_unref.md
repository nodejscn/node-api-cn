<!-- YAML
added: v9.7.0
-->

* 返回: {Immediate} 对 `immediate` 的引用。

调用时，活动的 `Immediate` 对象不需要 Node.js 事件循环保持活动状态。 
如果没有其他活动保持事件循环运行，则进程可以在调用 `Immediate` 对象的回调之前退出。 
多次调用 `immediate.unref()` 将无效。

