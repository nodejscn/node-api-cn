<!-- YAML
added: v0.5.9
-->

* `timeout` {number} 请求超时的毫秒数。
* `callback` {Function} 当超时发生时的回调函数。相当于绑定到 `'timeout'` 事件。
* 返回: {http.ClientRequest}

当 socket 被分配给请求且已连接，则 [`socket.setTimeout()`] 会被调用。


