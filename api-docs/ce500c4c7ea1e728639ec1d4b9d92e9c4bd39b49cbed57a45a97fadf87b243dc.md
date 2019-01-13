<!-- YAML
added: v0.11.4
-->

* `options` {Object} 包含连接详细信息的选项。 查看 [`net.createConnection()`] 以获取选项的格式。
* `callback` {Function} 接收创建的套接字的回调函数。
* 返回: {net.Socket}

生成用于 HTTP 请求的套接字或流。

默认情况下，此函数与 [`net.createConnection()`] 相同。 
但是，如果需要更大的灵活性，自定义代理可能会覆盖此方法。

可以通过以下两种方式之一提供套接字或流：通过从此函数返回套接字或流，或者通过将套接字或流传给 `callback`。

`callback` 的参数是 `(err, stream)`。

