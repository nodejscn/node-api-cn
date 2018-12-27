
[`child_process.spawn()`]、[`child_process.fork()`]、[`child_process.exec()`] 和 [`child_process.execFile()`] 都遵循 Node.js 惯用的异步编程模式。

每个方法都返回 [`ChildProcess`] 实例。
这些对象都实现了 [`EventEmitter`] 接口，允许父进程注册监听器函数，在子进程生命周期期间，当特定的事件发生时会调用这些函数。

`child_process.exec()` 和 `child_process.execFile()` 可以额外指定 `callback` 函数，当子进程结束时会被调用。

