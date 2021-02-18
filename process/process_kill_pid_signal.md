<!-- YAML
added: v0.0.6
-->

* `pid` {number} 进程 ID。
* `signal` {string|number} 要发送的信号，类型为字符串或数字。**默认值:** `'SIGTERM'`。

`process.kill()` 方法会发送 `signal` 到 `pid` 标识的进程。

信号名称为字符串（比如 `'SIGINT'` 或 `'SIGHUP'`）。
详见[信号事件][Signal Events]和 kill(2)。

如果目标 `pid` 不存在，则该方法会抛出错误。
作为特例，信号 `0` 可以用于测试进程是否存在。
在 Windows 平台上，如果 `pid` 被用于杀死进程组，则会抛出错误。

虽然此函数的名称是 `process.kill()`，它其实只是信号发送器，类似于 `kill` 系统调用。
发送的信号可以做一些与杀死目标进程无关的事情。

```js
process.on('SIGHUP', () => {
  console.log('收到 SIGHUP 信号');
});

setTimeout(() => {
  console.log('退出中');
  process.exit(0);
}, 100);

process.kill(process.pid, 'SIGHUP');
```

当 Node.js 进程接收到 `SIGUSR1` 时，Node.js 会启动调试器。
参见[信号事件][Signal Events]。

