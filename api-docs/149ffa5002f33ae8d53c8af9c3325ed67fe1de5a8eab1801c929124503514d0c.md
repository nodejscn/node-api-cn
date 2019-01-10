<!-- YAML
added: v0.9.1
-->

* Returns: {net.Socket} Socket 本身。

如果活跃的 socket 是事件系统中仅存的 socket，则调用 `unref` 将会允许程序退出。对一个已经调用了 `unref` 的 socket 再调用 `unref` 无效。
