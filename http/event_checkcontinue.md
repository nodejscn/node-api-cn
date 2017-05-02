<!-- YAML
added: v0.3.0
-->

* `request` {http.IncomingMessage}
* `response` {http.ServerResponse}

每当接收到一个带有 HTTP `Expect: 100-continue` 请求头的请求时触发。
如果该事件未被监听，则服务器会自动响应 `100 Continue`。

处理该事件时，如果客户端应该继续发送请求主体，则调用 [`response.writeContinue()`]，否则生成一个适当的 HTTP 响应（例如 400 错误请求）。

注意，当该事件被触发且处理后，[`'request'`] 事件不会被触发。

