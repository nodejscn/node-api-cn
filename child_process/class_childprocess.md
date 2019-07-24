<!-- YAML
added: v2.2.0
-->

`ChildProcess` 类的实例都是 [`EventEmitter`]，表示衍生的子进程。

`ChildProcess` 的实例不是直接创建的，而是使用 [`child_process.spawn()`]、[`child_process.exec()`]、[`child_process.execFile()`] 或 [`child_process.fork()`] 方法来创建 `ChildProcess` 的实例。

