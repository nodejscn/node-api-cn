<!-- YAML
added: v0.7.10
-->

默认情况下，父进程将会等待已分离的子进程退出。
为了防止父进程等待给定的 `subprocess` 退出，可使用 `subprocess.unref()` 方法。
这样做将会导致父进程的事件循环不会在其引用计数中包括子进程，允许父进程独立于子进程退出，除非子进程与父进程之间已建立了 IPC 通道。

```js
const { spawn } = require('child_process');

const subprocess = spawn(process.argv[0], ['child_program.js'], {
  detached: true,
  stdio: 'ignore'
});

subprocess.unref();
```

