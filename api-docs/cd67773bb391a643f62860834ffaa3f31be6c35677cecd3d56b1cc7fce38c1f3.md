<!-- YAML
added: v0.8.1
-->

* {boolean}

如果该进程是主进程，则为 `true`。
这是由 `process.env.NODE_UNIQUE_ID` 决定的。
如果 `process.env.NODE_UNIQUE_ID` 未定义，则 `isMaster` 为 `true`。

