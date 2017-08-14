<!-- YAML
added: v0.1.90
-->

* `signal` {string}

`subprocess.kill()` 方法向子进程发送一个信号。
如果没有给定参数，则进程会发送 `'SIGTERM'` 信号。
查看 signal(7) 了解可用的信号列表。

```js
const { spawn } = require('child_process');
const grep = spawn('grep', ['ssh']);

grep.on('close', (code, signal) => {
  console.log(`子进程收到信号 ${signal} 而终止`);
});

// 发送 SIGHUP 到进程
grep.kill('SIGHUP');
```

如果信号没有被送达，[`ChildProcess`] 对象可能会触发一个 [`'error'`] 事件。
向一个已经退出的子进程发送信号不是一个错误，但可能有无法预知的后果。
特别是，如果进程的 PID 已经重新分配给其他进程，则信号会被发送到该进程，从而可能有意想不到的结果。

注意，当函数被调用 `kill` 时，已发送到子进程的信号可能没有实际终止该进程。

详见 kill(2)。

注意：在 Linux 上，当试图杀死父进程时，子进程的子进程不会被终止。
这有可能发生在当在一个 shell 中运行一个新进程时，或使用 `ChildProcess` 中的 `shell` 选项时，例如：

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
  subprocess.kill(); // 不会终止 shell 中的 node 进程
}, 2000);
```

