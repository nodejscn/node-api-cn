<!-- YAML
added: v0.9.12
-->

* `signal` {string} 被发送kill信号的工作进程名称。

这个方法将会kill工作进程。在主进程中，通过断开与`worker.process`的连接来实现，一旦断开连接后，通过`signal`来杀死工作进程。在工作进程中，通过断开IPC管道来实现，然后以代码`0`退出进程。

将导致`.exitedAfterDisconnect`被设置。

为向后兼容，这个方法与`worker.destroy()`等义。

需要注意的是，在工作进程中有一个方法`process.kill()` ，这个方法本方法不同，本方法是[`kill`][]。

