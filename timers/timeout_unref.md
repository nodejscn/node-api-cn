<!-- YAML
added: v0.9.1
-->

* 返回: {Timeout} `timeout` 的引用。

当被调用时，活动的 `Timeout` 对象将不会要求 Node.js 事件循环保持活动状态。 
如果没有其他的活动保持事件循环运行，则进程可能会在 `Timeout` 对象的回调被调用之前退出。 
多次调用 `timeout.unref()` 没有影响。

调用 `timeout.unref()` 会创建一个内部的定时器，它将会唤醒 Node.js 事件循环。 
创建太多的这类定时器可能会对 Node.js 应用程序的性能产生负面的影响。


