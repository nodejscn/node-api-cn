<!-- YAML
added: v0.7.2
-->

* {boolean} 调用 `subprocess.disconnect()` 后会被设为 `false`

`subprocess.connected` 属性表明是否仍可以从一个子进程发送和接收消息。
当 `subprocess.connected` 为 `false` 时，则不能再发送或接收的消息。

<a name="child_process_child_disconnect"></a>
