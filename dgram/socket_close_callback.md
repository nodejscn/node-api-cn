<!-- YAML
added: v0.1.99
-->

* `callback` {Function} 当 socket 已被关闭时调用。

关闭该 socket 并停止监听其上的数据。
如果提供了一个回调函数，它就相当于为 [`'close'`] 事件添加了一个监听器。

