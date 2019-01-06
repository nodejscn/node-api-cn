<!-- YAML
added: v0.1.90
-->

* `code` {number} 子进程的退出码。
* `signal` {string} 终止子进程的信号。

当子进程结束后时触发。
如果进程退出，则 `code` 是进程的最终退出码，否则为 `null`。
如果进程是收到的信号而终止，则 `signal` 是信号的名称，否则为 `null`。
这两个值至少有一个是非空的。

当 `'exit'` 事件被触发时，子进程的 stdio 流可能依然是打开的。

Node.js 建立了 `SIGINT` 和 `SIGTERM` 的信号处理程序，且 Node.js 进程收到这些信号也不会立即终止。
Node.js 会执行一系列的清理操作后重新引发处理信号。

参阅 waitpid(2)。

