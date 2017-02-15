<!-- YAML
added: v2.2.0
-->

`ChildProcess` 类的实例是 [`EventEmitter`]，代表衍生的子进程。

`ChildProcess` 的实例不被直接创建。
而是，使用 [`child_process.spawn()`]、[`child_process.exec()`]、[`child_process.execFile()`] 或 [`child_process.fork()`] 方法创建 `ChildProcess` 实例。

