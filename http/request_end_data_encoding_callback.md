<!-- YAML
added: v0.1.90
-->

* `data` {String | Buffer}
* `encoding` {String}
* `callback` {Function}

完成发送请求。
如果主体的任何部分未被发送，则会刷新它们到流中。
如果请求被分块，则会发送终止 `'0\r\n\r\n'`。

如果指定了 `data`，则等同于调用 `request.end(callback)` 之后调用 [`response.write(data, encoding)`]。

如果指定了 `callback`，则当请求流结束时会被调用。

