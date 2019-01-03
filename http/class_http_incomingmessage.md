<!-- YAML
added: v0.1.17
-->

`http.IncomingMessage` 对象由 [`http.Server`] 或 [`http.ClientRequest`] 创建，并作为参数分别传入 [`'request'`] 和 [`'response'`] 事件。
可以用来访问响应状态、消息头、或数据。

`http.IncomingMessage` 类实现了[可读流][Readable Stream]接口。

