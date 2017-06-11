<!-- YAML
added: v0.7.2
-->

如果 Node.js 进程是从IPC频道派生出来的（具体看 [Child Process][] 和  [Cluster][] 的文档）, `process.disconnect()`函数会关闭到父进程的IPC频道，以允许子进程一旦没有其他链接来保持活跃就优雅地关闭。

调用`process.disconnect()`的效果和父进程调用`ChildProcess.disconnect()`的一样[`ChildProcess.disconnect()`][].

如果 Node.js 进程不是从IPC频道派生出来的，那调用`process.disconnect()`函数的结果是`undefined`. 
