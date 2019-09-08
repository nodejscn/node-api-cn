<!-- YAML
added: v0.1.17
-->

* 继承自: {stream.Readable}

`IncomingMessage` 对象由 [`http.Server`] 或 [`http.ClientRequest`] 创建，并分别作为第一个参数传给 [`'request'`] 和 [`'response'`] 事件。 
它可用于访问响应状态、消息头、以及数据。

