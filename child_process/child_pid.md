<!-- YAML
added: v0.1.90
-->

* {Number} 整数

返回子进程的进程标识（PID）。

例子：

```js
const spawn = require('child_process').spawn;
const grep = spawn('grep', ['ssh']);

console.log(`衍生的子进程的 pid：${grep.pid}`);
grep.stdin.end();
```

