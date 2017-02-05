<!-- YAML
added: v0.3.2
-->

当服务器发送了一个 `100 Continue` 的 HTTP 响应时触发，通常因为该请求包含 `Expect: 100-continue`。
这是客户端应发送请求主体的指令。

