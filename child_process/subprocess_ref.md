<!-- YAML
added: v0.7.10
-->

调用 `subprocess.unref()` 之后再调用 `subprocess.ref()` 会还原已被移除的子进程引用计数，强迫父进程在退出自身之前等待子进程退出。

```js
const { spawn } = require('child_process');

const subprocess = spawn(process.argv[0], ['child_program.js'], {
  detached: true,
  stdio: 'ignore'
});

subprocess.unref();
subprocess.ref();
```

