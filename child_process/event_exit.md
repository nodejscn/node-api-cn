<!-- YAML
added: v0.1.90
-->

* `code` {number} 子进程自行退出时的退出码。
* `signal` {string} 子进程被终止的信号。

当子进程结束后时会触发 `'exit'` 事件。
如果进程退出，则 `code` 是进程的最终退出码，否则为 `null`。
如果进程是因为收到的信号而终止，则 `signal` 是信号的字符串名称，否则为 `null`。
这两个值至少有一个是非 `null` 的。

当 `'exit'` 事件被触发时，子进程的 stdio 流可能依然是打开的。

Node.js 为 `SIGINT` 和 `SIGTERM` 建立了信号处理程序，且 Node.js 进程收到这些信号不会立即终止。
相反，Node.js 将会执行一系列的清理操作，然后再重新提升处理后的信号。

参见 waitpid(2)。

