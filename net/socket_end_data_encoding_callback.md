<!-- YAML
added: v0.1.90
-->

* `data` {string|Buffer|Uint8Array}
* `encoding` {string} 仅当 `data` 是字符串时有效。默认为 `'utf8'`。
* `callback` {Function} 当 socket 完成时的回调函数。
* 返回: {net.Socket} socket 本身。

半关闭 socket。
例如发送一个 FIN 包。
服务端仍可以发送数据。

如果指定了 `data`，则相当于调用 `socket.write(data, encoding)` 之后再调用 [`socket.end()`]。

