<!-- YAML
added: v0.1.90
-->

* {number} 整数

返回子进程的进程标识（PID）。

例子：

```js
const { spawn } = require('child_process');
const grep = spawn('grep', ['ssh']);

console.log(`衍生的子进程的 pid：${grep.pid}`);
grep.stdin.end();
```

<a name="child_process_child_send_message_sendhandle_options_callback"></a>

