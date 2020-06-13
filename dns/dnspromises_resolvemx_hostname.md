<!-- YAML
added: v10.6.0
-->

* `hostname` {string}

使用DNS协议解析`hostname`的邮件交换记录（`MX`记录）。 成功后，`Promise`将通过一系列包含`优先级`和`交换`属性的对象来解决（例如，`[{priority: 10, exchange: 'mx.example.com'}, ...]` ）。
