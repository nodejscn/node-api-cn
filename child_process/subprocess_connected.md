<!-- YAML
added: v0.7.2
-->

* {boolean} 调用 `subprocess.disconnect()` 后会被设为 `false`。

表明是否可以从子进程发送和接收消息。
当 `subprocess.connected` 为 `false` 时，则不能再发送或接收消息。

