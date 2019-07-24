<!-- YAML
added: v0.5.10
-->

* {boolean} 当使用 `subprocess.kill()` 成功发送信号到子进程后，该值会被设为 `true`。

`subprocess.killed` 属性表明子进程是否已成功接收到来着 `subprocess.kill()` 的信号。
`killed` 属性并不表明子进程是否已被终止。


