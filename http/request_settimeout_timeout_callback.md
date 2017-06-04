<!-- YAML
added: v0.5.9
-->

* `timeout` {number} 请求被认为是超时的毫秒数。
* `callback` {Function} 可选的函数，当超时发生时被调用。等同于绑定到 `timeout` 事件。

一旦 socket 被分配给请求且已连接，[`socket.setTimeout()`] 会被调用。

返回 `request`。

