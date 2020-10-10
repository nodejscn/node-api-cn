<!-- YAML
added: v0.9.12
changes:
  - version: v13.0.0
    pr-url: https://github.com/nodejs/node/pull/27558
    description: The default timeout changed from 120s to 0 (no timeout).
-->

* `msecs` {number} **默认值:** `120000`（2 分钟）。
* `callback` {Function}
* 返回: {http.Server}

设置套接字的超时值，并在服务器对象上触发 `'timeout'` 事件，如果发生超时，则将套接字作为参数传入。

如果服务器对象上有 `'timeout'` 事件监听器，则将使用超时的套接字作为参数调用它。

默认情况下，服务器不会使 socket 超时。 
但是，如果将回调分配给服务器的 `'timeout'` 事件，则必须显式处理超时。


