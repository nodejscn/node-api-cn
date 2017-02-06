<!-- YAML
added: v0.1.90
-->

* `data` {String | Buffer}
* `encoding` {String}
* `callback` {Function}

该方法告诉服务器所有响应头和主体都已被发送；服务器应将消息视为已完成。
对于每个响应，`response.end()` 方法**必须**被调用。

如果指定了 `data`，则它等同于调用 [`response.write(data, encoding)`] 之后调用 `response.end(callback)`。

如果指定了 `callback`，则当响应流结束时被调用。

