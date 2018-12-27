<!-- YAML
added: v0.7.2
-->

调用父进程的 [`subprocess.disconnect()`] 或子进程的 [`process.disconnect()`] 后会触发。
断开连接后就不能再发送或接收信息，且 [`subprocess.connected`] 属性会被设为 `false`。

