<!-- YAML
added: v0.11.4
-->

* `options` {Object} 包含连接详情的选项。详见 [`net.createConnection()`] 了解选项的格式
* `callback` {Function} 接收创建的 socket 的回调函数
* 返回: {net.Socket}

生产一个用于 HTTP 请求的 socket/stream。

默认情况下，该函数类似于 [`net.createConnection()`]。
但是，如果期望更大的灵活性，自定义代理可以重写此方法。

socket/stream 可以由以下两个方法提供：从该函数返回 socket/stream，或传入 `callback` 的 socket/stream。

`callback` 有 `(err, stream)` 参数。

