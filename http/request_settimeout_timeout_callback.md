<!-- YAML
added: v0.5.9
-->

* `timeout` {Number} 一个请求被认为是超时的毫秒数。
* `callback` {Function} 可选的函数，当发生超时时调用。与绑定到 `timeout` 事件的相同。

一旦 socket 被分配给请求且已连接，[`socket.setTimeout()`] 会被调用。

返回 `request`。

