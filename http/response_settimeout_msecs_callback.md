<!-- YAML
added: v0.9.12
-->

* `msecs` {number}
* `callback` {Function}

设置 socket 的超时时间为 `msecs`。
如果提供了回调函数，则它会作为监听器被添加到响应对象的 `'timeout'` 事件。

如果没有 `'timeout'` 监听器被添加到请求、响应或服务器，则 socket 会在超时后被销毁。
如果在请求、响应或服务器的 `'timeout'` 事件上分配了回调函数，则超时的 socket 必须被显式地处理。

返回 `response`。

