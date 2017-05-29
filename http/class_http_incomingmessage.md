<!-- YAML
added: v0.1.17
-->

`IncomingMessage` 对象由 [`http.Server`] 或 [`http.ClientRequest`] 创建，并作为第一个参数分别递给 [`'request'`] 和 [`'response'`] 事件。
它可以用来访问响应状态、消息头、以及数据。

它实现了 [可读流] 接口，还有以下额外的事件、方法、以及属性。

