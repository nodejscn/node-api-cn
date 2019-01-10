<!-- YAML
added: v0.3.2
-->

当服务器发送了一个 `100 Continue` 的 HTTP 响应时触发，通常是因为请求包含 `Expect: 100-continue`。
这是客户端将要发送请求主体的指令。

