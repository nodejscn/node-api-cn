<!-- YAML
added: v10.6.0
-->

* `hostname` {string}

使用DNS协议解析`hostname`的`CNAME`记录。 成功完成后，将使用一系列可用于主机名的规范名称记录来解决`Promise`（例如 `['bar.example.com']）。
