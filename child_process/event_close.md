<!-- YAML
added: v0.7.7
-->

* `code` {number} 子进程的退出码。
* `signal` {string} 终止子进程的信号。

当子进程的 stdio 流被关闭时触发。
与 [`'exit'`] 事件的区别是，多个进程可能共享同一 stdio 流。

