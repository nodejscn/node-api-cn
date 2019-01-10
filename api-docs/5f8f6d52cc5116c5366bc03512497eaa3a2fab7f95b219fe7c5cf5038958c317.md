<!-- YAML
added: v0.9.1
-->
调用时，只要 `Timeout` 处于活动状态就要求 Node.js 事件循环不要退出。
多次调用 `timeout.ref()` 没有效果。

注意：默认情况下，所有 `Timeout` 对象都是 "ref'd" 的，通常不需要调用 `timeout.ref()`，除非之前调用了 `timeout.unref()`。

返回 `Timeout` 的一个引用。

