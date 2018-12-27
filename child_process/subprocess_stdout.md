<!-- YAML
added: v0.1.90
-->

* {stream.Readable}

返回子进程的 `stdout` 可读流。

如果衍生子进程时 `stdio[1]` 被设为不是 `'pipe'` 的值，则返回 `null`。

`subprocess.stdout` 是 `subprocess.stdio[1]` 的别名。
两个属性指向同一个值。

