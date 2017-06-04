<!-- YAML
added: v0.9.12
-->

* `msecs` {number} 默认为 120000 (2 分钟)。
* `callback` {Function}

设置 socket 的超时时间。
如果发生超时，则触发服务器对象的 `'timeout'` 事件，并传入 socket 作为一个参数。

默认情况下，服务器的超时时间是 2 分钟，且超时后的 socket 会被自动销毁。
但是，如果你为服务器的 `'timeout'` 事件分配了一个回调函数，则超时必须被显式地处理。

返回 `server`。

