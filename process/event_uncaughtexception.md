<!-- YAML
added: v0.1.18
-->

如果 Javascript 未捕获的异常，沿着代码调用路径反向传递回事件循环，会触发 `'uncaughtException'` 事件。
Node.js 默认情况下会将这些异常堆栈打印到 `stderr` 然后进程退出。
为 `'uncaughtException'` 事件增加监听器会覆盖上述默认行为。

`'uncaughtException'` 事件监听器的回调函数，使用 `Error` 对象作为唯一参数值。

例如:

```js
process.on('uncaughtException', (err) => {
  fs.writeSync(1, `捕获到异常：${err}\n`);
});

setTimeout(() => {
  console.log('这里仍然会运行。');
}, 500);

// 故意调用一个不存在的函数，应用会抛出未捕获的异常。
nonexistentFunc();
console.log('这里不会运行。');
```

