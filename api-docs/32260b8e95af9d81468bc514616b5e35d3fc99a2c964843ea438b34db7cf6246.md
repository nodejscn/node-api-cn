<!-- YAML
added: v0.1.17
-->

`IncomingMessage` 对象由 [`http.Server`] 或 [`http.ClientRequest`] 创建，并分别作为第一个参数传给 [`'request'`] 和 [`'response'`] 事件。 
它可用于访问响应状态、消息头、以及数据。

它实现了[可读流][Readable Stream]接口，还有以下额外的事件、方法、以及属性。

