<!-- YAML
added: v0.9.1
-->

当调用时，活动的 `Timeout` 对象不要求 Node.js 事件循环保持活动。
如果没有其他活动保持事件循环运行，则进程可能在 `Timeout` 对象的回调被调用之前退出。
多次调用 `timeout.unref()` 没有效果。

注意：调用 `timeout.unref()` 会创建一个内部定时器，它会唤醒 Node.js 的事件循环。
创建太多这类定时器可能会对 Node.js 应用程序的性能产生负面影响。

返回对 `Timeout` 的一个引用。

