<!-- YAML
added: v0.1.90
-->

* {integer}

返回子进程的进程标识（PID）。

```js
const { spawn } = require('child_process');
const grep = spawn('grep', ['ssh']);

console.log(`衍生的子进程的 pid：${grep.pid}`);
grep.stdin.end();
```

