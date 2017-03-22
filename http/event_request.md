<!-- YAML
added: v0.1.0
-->

* `request` {http.IncomingMessage}
* `response` {http.ServerResponse}

每次接收到一个请求时触发。
注意，每个连接可能有多个请求（在 HTTP `keep-alive` 连接的情况下）。

