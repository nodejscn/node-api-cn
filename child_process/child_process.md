
<!--introduced_in=v0.10.0-->
<!--lint disable maximum-line-length-->

> 稳定性: 2 - 稳定的

`child_process` 模块提供了衍生子进程的功能，与 popen(3) 类似但不完全相同。
主要由 [`child_process.spawn()`] 提供：

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

默认情况下，Node.js 的父进程与衍生的子进程之间会建立 `stdin`、`stdout` 和 `stderr` 的管道。

[`child_process.spawn()`] 用于异步地衍生子进程，且不会阻塞 Node.js 事件循环。
[`child_process.spawnSync()`] 则同步地衍生子进程，但会阻塞事件循环直到衍生的子进程退出或被终止。

`child_process` 模块还提供了其他一些同步和异步的方法。
每个方法都是基于 `child_process.spawn()` 或 `child_process.spawnSync()` 实现的。

  * [`child_process.exec()`]: 衍生一个 shell 并在 shell 上运行命令，当完成时传入 `stdout` 和 `stderr` 到回调函数。
  * [`child_process.execFile()`]: 类似 `child_process.exec()`，但直接衍生命令且无需先衍生 shell。
  * [`child_process.fork()`]: 衍生一个新的 Node.js 进程，并通过 IPC 通讯通道来调用指定的模块，该通道允许父进程与子进程之间相互发送信息。
  * [`child_process.execSync()`]: `child_process.exec()` 的同步版本，会阻塞 Node.js 事件循环。
  * [`child_process.execFileSync()`]: `child_process.execFile()` 的同步版本，会阻塞 Node.js 事件循环。

对于某些用例，比如自动化的 shell 脚本，[同步的方法][synchronous counterparts]更方便。
但大多数情况下，同步的方法会明显影响性能，因为它会拖延事件循环直到衍生进程完成。


