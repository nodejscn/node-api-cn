<!-- YAML
added: v0.1.90
-->

* Returns: {net.Socket}

确保在该 socket 上不再有 I/O 活动。仅在出现错误的时候才需要（如解析错误等）。

如果制定了 `exception`，则将会触发一个 [`'error'`][] 事件，任何监听器都将接收到 `exception` 作为一个参数。
