<!-- YAML
added: v0.1.90
-->

* {stream.Readable}

表示子进程的 `stderr` 的可读流。

如果子进程被衍生时 `stdio[2]` 被设置为 `'pipe'` 以外的任何值，则该值将会是 `null`。

`subprocess.stderr` 是 `subprocess.stdio[2]` 的别名。
两个属性都将会指向相同的值。

