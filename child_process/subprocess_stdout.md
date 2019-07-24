<!-- YAML
added: v0.1.90
-->

* {stream.Readable}

表示子进程的 `stdout` 的可读流。

如果子进程被衍生时 `stdio[1]` 被设置为 `'pipe'` 以外的任何值，则该值将会是 `null`。

`subprocess.stdout` 是 `subprocess.stdio[1]` 的别名。
两个属性都将会指向相同的值。

```js
const { spawn } = require('child_process');

const subprocess = spawn('ls');

subprocess.stdout.on('data', (data) => {
  console.log(`接收到数据块 ${data}`);
});
```

