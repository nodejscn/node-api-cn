<!-- YAML
added: v0.7.2
-->

在父进程中调用 [`subprocess.disconnect()`] 或在子进程中调用 [`process.disconnect()`] 后会触发 `'disconnect'` 事件。
断开后就不能再发送或接收信息，且 [`subprocess.connected`] 属性会被设为 `false`。

