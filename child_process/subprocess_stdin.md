<!-- YAML
added: v0.1.90
-->

* {stream.Writable}

一个代表子进程的 `stdin` 的可写流。

注意，如果一个子进程正在等待读取所有的输入，则子进程不会继续直到流已通过 `end()` 关闭。

如果子进程被衍生时 `stdio[0]` 被设为任何不是 `'pipe'` 的值，则这会是 `null`。

`subprocess.stdin` 是 `subprocess.stdio[0]` 的一个别名。
这两个属性指向相同的值。

<a name="child_process_child_stdio"></a>
