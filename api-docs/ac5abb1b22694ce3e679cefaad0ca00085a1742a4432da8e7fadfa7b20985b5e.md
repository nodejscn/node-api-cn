<!-- YAML
added: v0.3.0
-->

每当 `input` 流接收到一个 `<ctrl>-C` 输入（通常被称为 `SIGINT`）时，触发 `'SIGINT'` 事件。
当 `input` 流接收到一个 `SIGINT` 时，如果没有注册 `'SIGINT'` 事件监听器，则 `'pause'` 事件会被触发。

监听器函数被调用时不传入任何参数。

例子：

```js
rl.on('SIGINT', () => {
  rl.question('确定要退出吗？ ', (answer) => {
    if (answer.match(/^y(es)?$/i)) rl.pause();
  });
});
```

