<!-- YAML
added: v2.2.0
-->

* 继承自: {EventEmitter}

`ChildProcess` 的实例代表衍生的子进程。

`ChildProcess` 的实例不是直接创建的。
而是，使用 [`child_process.spawn()`]、[`child_process.exec()`]、[`child_process.execFile()`] 或 [`child_process.fork()`] 方法来创建 `ChildProcess` 的实例。

