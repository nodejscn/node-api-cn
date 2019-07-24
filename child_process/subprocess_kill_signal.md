<!-- YAML
added: v0.1.90
-->

* `signal` {number|string}

`subprocess.kill()` 方法会向子进程发送一个信号。
如果没有给定参数，则进程将会发送 `'SIGTERM'` 信号。
参阅 signal(7) 了解可用的信号列表。

```js
const { spawn } = require('child_process');
const grep = spawn('grep', ['ssh']);

grep.on('close', (code, signal) => {
  console.log(`子进程因收到信号 ${signal} 而终止`);
});

// 发送 SIGHUP 到进程。
grep.kill('SIGHUP');
```

如果信号没有被送达，则 [`ChildProcess`] 对象可能会触发 [`'error'`] 事件。
向一个已经退出的子进程发送信号不是一个错误，但可能有无法预料的后果。
具体来说，如果进程的标识符 PID 已经被重新分配给其他进程，则信号将会被发送到该进程，而这可能产生意外的结果。

虽然该函数被称为 `kill`，但传给子进程的信号可能实际上不会终止该进程。

参阅 kill(2)。

在 Linux 上，子进程的子进程在试图杀死其父进程时将不会被终止。
当在 shell 中运行新进程、或使用 `ChildProcess` 的 `shell` 选项时，可能会发生这种情况：

```js
'use strict';
const { spawn } = require('child_process');

const subprocess = spawn(
  'sh',
  [
    '-c',
    `node -e "setInterval(() => {
      console.log(process.pid, 'is alive')
    }, 500);"`
  ], {
    stdio: ['inherit', 'inherit', 'inherit']
  }
);

setTimeout(() => {
  subprocess.kill(); // 不会终止 shell 中的 node 进程。
}, 2000);
```

