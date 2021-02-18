<!-- YAML
added: v0.1.18
changes:
  - version:
     - v12.0.0
     - v10.17.0
    pr-url: https://github.com/nodejs/node/pull/26599
    description: 添加 `origin` 参数。
-->

* `err` {Error} 未捕获的异常。
* `origin` {string} 表明异常的来源（来自未处理的拒绝、或来自同步的错误）。
  可以是 `'uncaughtException'` 或 `'unhandledRejection'`。
  后者仅用于 [`--unhandled-rejections`] 标志被设置为 `strict` 或 `throw` 且有未处理的拒绝。

当未捕获的 JavaScript 异常冒泡回到事件循环时，则会触发 `'uncaughtException'` 事件。 
默认情况下，Node.js 会这样处理此类异常：打印堆栈跟踪到 `stderr` 并使用退出码 `1` 来退出，且会覆盖任何先前设置的 [`process.exitCode`]。 
为 `'uncaughtException'` 事件添加句柄会覆盖此默认行为。 
另外，如果在 `'uncaughtException'` 句柄中更改 [`process.exitCode`]，则会使进程以提供的退出码退出。 
否则，在存在这样的句柄的情况下，进程会以退出码 `0` 退出。

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

通过添加 `'uncaughtExceptionMonitor'` 事件监听器，可以监视 `'uncaughtException'` 事件但不覆盖默认的退出进程的行为。

