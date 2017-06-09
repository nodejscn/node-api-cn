<!-- YAML
added: v0.1.18
-->

如果Javascript未捕获的异常，沿着代码调用路径反向传递回event loop，会触发`'uncaughtException'`事件。
Node.js默认情况下会将这些异常堆栈打印到`stderr` 然后进程退出。
为`'uncaughtException'`事件增加监听器会覆盖上述默认行为。

`'uncaughtException'`事件监听器的回调函数，使用`Error` object作为唯一参数值。

例如:

```js
process.on('uncaughtException', (err) => {
  fs.writeSync(1, `Caught exception: ${err}\n`);
});

setTimeout(() => {
  console.log('This will still run.');
}, 500);

// 故意调用一个不存在的函数，应用会抛出未捕获的异常
nonexistentFunc();
console.log('This will not run.');
```

