<!-- YAML
added: v0.11.4
-->

* `options` {Object} 包含连接详情的选项。查看 [`net.createConnection()`] 了解选项的格式。
* `callback` {Function} 接收被创建的 socket 的回调函数。
* 返回: {net.Socket}

创建一个用于 HTTP 请求的 socket 或流。

默认情况下，该函数类似于 [`net.createConnection()`]。
但是如果期望更大的灵活性，自定义的代理可以重写该方法。

socket 或流可以通过以下两种方式获取：从该函数返回，或传入 `callback`。

`callback` 有 `(err, stream)` 参数。

