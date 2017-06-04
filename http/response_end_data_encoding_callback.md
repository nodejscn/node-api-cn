<!-- YAML
added: v0.1.90
-->

* `data` {string | Buffer}
* `encoding` {string}
* `callback` {Function}

该方法会通知服务器，所有响应头和响应主体都已被发送，即服务器将其视为已完成。
每次响应都必须调用 `response.end()` 方法。

如果指定了 `data`，则相当于调用 [`response.write(data, encoding)`] 之后再调用 `response.end(callback)`。

如果指定了 `callback`，则当响应流结束时被调用。

