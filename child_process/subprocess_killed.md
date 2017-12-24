<!-- YAML
added: v0.5.10
-->

* {boolean} 当 `subprocess.kill()` 已成功发送信号给子进程后会被设置为 `true`。

`subprocess.killed` 属性表明该子进程是否已成功接收到 `subprocess.kill()` 的信号。
该属性不代表子进程是否已被终止。

<a name="child_process_child_pid"></a>
