<!-- YAML
added: v0.0.6
-->

* `pid` {number} 进程ID
* `signal` {string|number} 将发送的信号，类型为string或number。默认为`'SIGTERM'`。

`process.kill()`方法将`signal`发送给`pid`标识的进程。

信号名称是如`'SIGINT'` 或 `'SIGHUP'`的字符串。更多信息，查看[Signal Events][] 和 kill(2)。

如果目标`pid`不存在，该方法会抛出错误。作为一个特殊例子，信号`0`可以用于测试进程是否存在。
在Windows平台中，如果`pid`用于kill进程组，会抛出错误。

*注意*：即使这个函数的名称是`process.kill()`,它其实只是发送信号，这点与`kill`系统调用类似。
发送的信号可能是做一些与kill目标进程无关的事情。

例如:

```js
process.on('SIGHUP', () => {
  console.log('Got SIGHUP signal.');
});

setTimeout(() => {
  console.log('Exiting.');
  process.exit(0);
}, 100);

process.kill(process.pid, 'SIGHUP');
```

*注意*: 当Node.js进程接收到了`SIGUSR1`，Node.js会启动debugger，查看[Signal Events][]。

