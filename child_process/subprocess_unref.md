<!-- YAML
added: v0.7.10
-->

默认情况下，父进程会等待已解绑的子进程退出。
如果无需父进程等待，可使用 `subprocess.unref()` 退出 `subprocess`。

```js
const { spawn } = require('child_process');

const subprocess = spawn(process.argv[0], ['child_program.js'], {
  detached: true,
  stdio: 'ignore'
});

subprocess.unref();
```

