<!-- YAML
added: v0.7.7
-->

* `code` {number} 如果子进程退出自身，则该值是退出码。
* `signal` {string} 子进程被终止时的信号。

当子进程的 stdio 流被关闭时会触发 `'close'` 事件。
这与 [`'exit'`] 事件不同，因为多个进程可能共享同一 stdio 流。

