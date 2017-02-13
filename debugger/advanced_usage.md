
启用和访问调试器的另一种方式，是启动 Node.js 时带上 `--debug` 命令行标志，或向一个已存在的 Node.js 进程发送 `SIGUSR1` 信号。

一旦一个进程以这种方式被设为调试模式，它就可以被 Node.js 调试器使用，通过连接到正在运行的进程的 `pid` 或通过正在监听的调试器的 URI 引用：

* `node debug -p <pid>` - 通过 `pid` 连接进程
* `node debug <URI>` - 通过 URI 连接进程，如 localhost:5858

