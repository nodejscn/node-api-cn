<!-- YAML
added: v5.5.0
-->

* `request` {http.ClientRequest}
* `response` {http.ServerResponse}

每当接收到一个带有 HTTP `Expect` 请求头的请求时触发，其中值不是 `100-continue`。
如果该事件未被监听，则服务器会自动响应 `417 Expectation Failed`。

注意，当该事件被触发且处理后，[`'request'`] 事件不会被触发。

