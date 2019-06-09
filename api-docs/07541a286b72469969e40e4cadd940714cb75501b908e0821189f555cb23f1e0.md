<!-- YAML
added: v0.1.90
-->

* {stream.Writable}

表示子进程的 `stdin` 的可写流。

如果子进程等待读取其所有的输入，则子进程将不会继续，直到流已通过 `end()` 关闭。

如果子进程被衍生时 `stdio[0]` 被设置为 `'pipe'` 以外的任何值，则该值将会是 `null`。

`subprocess.stdin` 是 `subprocess.stdio[0]` 的别名。
两个属性都将会指向相同的值。

