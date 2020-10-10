<!-- YAML
added: v0.1.17
changes:
  - version:
     - v13.1.0
     - v12.16.0
    pr-url: https://github.com/nodejs/node/pull/30135
    description: 属性 `readableHighWaterMark` 的值映射了 socket 中的值。
-->

* 继承自: {stream.Readable}

`IncomingMessage` 对象由 [`http.Server`] 或 [`http.ClientRequest`] 创建，并分别作为第一个参数传给 [`'request'`] 和 [`'response'`] 事件。 
它可用于访问响应状态、消息头、以及数据。

