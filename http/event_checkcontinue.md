<!-- YAML
added: v0.3.0
-->

* `request` {http.IncomingMessage}
* `response` {http.ServerResponse}

每次收到 HTTP `Expect: 100-continue` 的请求时都会触发。 
如果未监听此事件，服务器将自动响应 `100 Continue`。

处理此事件时，如果客户端应继续发送请求主体，则调用 [`response.writeContinue()`]，如果客户端不应继续发送请求主体，则生成适当的 HTTP 响应（例如 `400 Bad Request`）。

请注意，在触发和处理此事件时，不会触发 [`'request'`] 事件。

