<!-- YAML
added: v0.9.1
-->

* 返回: {net.Server}

如果这个 server 在事件系统中是唯一有效的，那么对 server 调用 `unref()` 将允许程序退出。
如果这个 server 已经调用过 `unref` 那么再次调用 `unref()` 将不会再有效果。
