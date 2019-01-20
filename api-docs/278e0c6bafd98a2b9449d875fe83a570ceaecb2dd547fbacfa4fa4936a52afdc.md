<!-- YAML
added: v5.5.0
-->

* `request` {http.IncomingMessage}
* `response` {http.ServerResponse}

每次收到带有 HTTP `Expect` 请求头的请求时触发，其中值不是 `100-continue`。 
如果未监听此事件，则服务器将根据需要自动响应 `417 Expectation Failed`。

请注意，在触发和处理此事件时，不会触发 [`'request'`] 事件。

