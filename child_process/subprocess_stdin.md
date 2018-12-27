<!-- YAML
added: v0.1.90
-->

* {stream.Writable}

返回子进程的 `stdin` 可写流。

如果子进程正在等待读取输入，则子进程不会继续直到流已通过 `end()` 关闭。

如果衍生子进程时 `stdio[0]` 被设为不是 `'pipe'` 的值，则返回 `null`。

`subprocess.stdin` 是 `subprocess.stdio[0]` 的别名。
两个属性指向同一个值。

