<!-- YAML
added: v0.1.90
-->

* {stream.Readable}

一个代表子进程的 `stderr` 的可读流。

如果子进程被衍生时 `stdio[2]` 被设为任何不是 `'pipe'` 的值，则这会是 `null`。

`child.stderr` 是 `child.stdio[2]` 的一个别名。
这两个属性指向相同的值。

