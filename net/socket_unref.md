<!-- YAML
added: v0.9.1
-->

在socket上调用 `unref`将允许程序当这是事件系统中唯一存活的socket时退出。
如果socket已经是`unref`，再次调用`unref`没有任何效应.

返回 `socket`.

