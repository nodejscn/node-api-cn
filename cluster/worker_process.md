<!-- YAML
added: v0.7.0
-->

* {ChildProcess}

所有的工作进程都是通过[`child_process.fork()`][]来创建的，这个方法返回的对象被存储为`.process`。在工作进程中， `process`属于全局对象。

详见：[Child Process module][]

需要注意：当`process`上发生 `'disconnect'`事件，并且`.exitedAfterDisconnect`的值不是`true`时，工作进程会调用 `process.exit(0)`。这样就可以防止连接意外断开。

