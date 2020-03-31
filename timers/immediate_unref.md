<!-- YAML
added: v9.7.0
-->

* 返回: {Immediate} `immediate` 的引用。

当被调用时，活动的 `Immediate` 对象将不会要求 Node.js 事件循环保持活动状态。 
如果没有其他的活动保持事件循环运行，则进程可能会在 `Immediate` 对象的回调被调用之前退出。 
多次调用 `immediate.unref()` 没有影响。

