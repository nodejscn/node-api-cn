<!-- YAML
added: v0.1.90
-->

* `callback` {Function} 当 server 被关闭时调用。
* 返回: {net.Server}

阻止 server 接受新的连接并保持现有的连接。
该函数是异步的，server 将在所有连接结束后关闭并触发 [`'close'`] 事件。
可选的 `callback` 将在 `'close'` 事件发生时被调用。
与 `'close'` 事件不同的是，如果 server 在关闭时未打开，回调函数被调用时会传入一个 `Error` 对象作为唯一参数。

