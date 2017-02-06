<!-- YAML
added: v0.9.12
-->

* `msecs` {Number}
* `callback` {Function}

设置 socket 的超时时间为 `msecs`。
如果提供了回调函数，则它会被作为监听器添加到响应对象的 `'timeout'` 事件。

如果没有 `'timeout'` 监听器被添加到请求、响应或服务器，则 socket 会在超时后被销毁。
如果在请求、响应或服务器的 `'timeout'` 事件上分配了句柄，则需要负责处理超时的 socket。

返回 `response`。

