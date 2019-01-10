<!-- YAML
added: v0.1.0
-->

* `request` {http.IncomingMessage}
* `response` {http.ServerResponse}

当接收到请求时触发。
每个连接可能有多个请求（在 HTTP `keep-alive` 的情况下）。

