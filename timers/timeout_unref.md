<!-- YAML
added: v0.9.1
-->

* 返回: {Timeout} 对 `timeout` 的引用。

调用时，活动的 `Timeout` 对象不需要 Node.js 事件循环保持活动状态。 
如果没有其他活动保持事件循环运行，则进程可以在调用 `Timeout` 对象的回调之前退出。 
多次调用 `timeout.unref()` 将无效。

调用 `timeout.unref()` 会创建一个内部定时器，它将唤醒 Node.js 事件循环。 
创建太多这些定时器可能会对 Node.js 应用程序的性能产生负面影响。


