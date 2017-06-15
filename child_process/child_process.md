
> 稳定性: 2 - 稳定的

`child_process` 模块提供了衍生子进程的功能，它与 popen(3) 类似，但不完全相同。
这个功能主要由 [`child_process.spawn()`] 函数提供：

```js
const { spawn } = require('child_process');
const ls = spawn('ls', ['-lh', '/usr']);

ls.stdout.on('data', (data) => {
  console.log(`输出：${data}`);
});

ls.stderr.on('data', (data) => {
  console.log(`错误：${data}`);
});

ls.on('close', (code) => {
  console.log(`子进程退出码：${code}`);
});
```

默认情况下，在 Node.js 的父进程与衍生的子进程之间会建立 `stdin`、`stdout` 和 `stderr` 的管道。
数据能以非阻塞的方式在管道中流通。
注意，有些程序会在内部使用行缓冲 I/O。
虽然这并不影响 Node.js，但这意味着发送到子过程的数据可能无法被立即使用。

[`child_process.spawn()`] 方法会异步地衍生子进程，且不会阻塞 Node.js 事件循环。
[`child_process.spawnSync()`] 方法则以同步的方式提供同样的功能，但会阻塞事件循环，直到衍生的子进程退出或终止。

为了方便起见，`child_process` 模块提供了一些同步和异步的替代方法用于  `child_process.spawn()` 和 `child_process.spawnSync()`。
注意，每个替代方法都是在 `child_process.spawn()` 或 `child_process.spawnSync()` 的基础上实现的。


  * [`child_process.exec()`]: 衍生一个 shell 并在 shell 上运行命令，当完成时会传入 `stdout` 和 `stderr` 到回调函数。
  * [`child_process.execFile()`]: 类似 `child_process.exec()`，但直接衍生命令，且无需先衍生一个 shell。
  * [`child_process.fork()`]: 衍生一个新的 Node.js 进程，并通过建立一个 IPC 通讯通道来调用一个指定的模块，该通道允许父进程与子进程之间相互发送信息。
  * [`child_process.execSync()`]: `child_process.exec()` 的同步方法，会阻塞 Node.js 事件循环。
  * [`child_process.execFileSync()`]: `child_process.execFile()` 的同步方法，会阻塞 Node.js 事件循环。

对于某些用例，如自动化的 shell 脚本，[同步的方法] 可能更方便。
大多数情况下，同步的方法会明显影响性能，因为它会拖延事件循环直到衍生进程完成。

