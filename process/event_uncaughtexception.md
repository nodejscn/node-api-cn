<!-- YAML
added: v0.1.18
changes:
  - version:
     - v12.0.0
     - v10.17.0
    pr-url: https://github.com/nodejs/node/pull/26599
    description: Added the `origin` argument.
-->

* `err` {Error} 未捕获的异常。
* `origin` {string} 表明异常是来自未处理的拒绝还是来自同步的错误。 可以是 `'uncaughtException'` 或 `'unhandledRejection'`。
  The latter is only used in conjunction with the
  [`--unhandled-rejections`][] flag set to `strict` or `throw` and
  an unhandled rejection.

当未捕获的 JavaScript 异常一直冒泡回到事件循环时，会触发 `'uncaughtException'` 事件。 
默认情况下，Node.js 通过将堆栈跟踪打印到 `stderr` 并使用退出码 `1` 来处理此类异常，从而覆盖任何先前设置的 [`process.exitCode`]。 
为 `'uncaughtException'` 事件添加处理程序会覆盖此默认行为。 
或者，更改 `'uncaughtException'` 处理程序中的 [`process.exitCode`]，这将导致进程退出并提供退出码。 
否则，在存在这样的处理程序的情况下，进程将以 `0` 退出。

```js
process.on('uncaughtException', (err, origin) => {
  fs.writeSync(
    process.stderr.fd,
    `捕获的异常: ${err}\n` +
    `异常的来源: ${origin}`
  );
});

setTimeout(() => {
  console.log('这里仍然会运行');
}, 500);

// 故意引起异常，但不要捕获它。
nonexistentFunc();
console.log('这里不会运行');
```

通过安装 `'uncaughtExceptionMonitor'` 监听器，可以监视 `'uncaughtException'` 事件，而不会覆盖默认行为以退出该进程。

