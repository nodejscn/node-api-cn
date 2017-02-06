<!-- YAML
added: v0.9.12
-->

* `msecs` {Number}
* `callback` {Function}

为 socket 设置超时值。
如果一个超时发生，则 Server 对象上会触发一个 `'timeout'` 事件，并传入该 socket 作为一个参数。

如果 Server 对象上有 `'timeout'` 事件监听器，则它会被调用，并带上超时的 socket 作为一个参数。

默认情况下，服务器的超时时间是 2 分钟，且超时后的 socket 会被自动销毁。
但是，如果你为服务器的 `'timeout'` 事件分配了一个回调函数，则你需要负责处理 socket 的超时。

返回 `server`。

