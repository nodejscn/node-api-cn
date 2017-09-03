<!-- YAML
added: v0.1.90
-->

* {stream.Readable}

一个代表子进程的 `stdout` 的可读流。

如果子进程被衍生时 `stdio[1]` 被设为任何不是 `'pipe'` 的值，则这会是 `null`。

`subprocess.stdout` 是 `subprocess.stdio[1]` 的一个别名。
这两个属性指向相同的值。

