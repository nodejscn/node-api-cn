<!-- YAML
added: v0.3.0
-->

每当 `input` 流接收到 `<ctrl>-C` 输入（通常称为 `SIGINT`）时，就会触发 `'SIGINT'` 事件。
如果当 `input` 流接收到 `SIGINT` 时没有注册 `'SIGINT'` 事件监听器，则会触发 `'pause'` 事件。

调用监听器函数时不传入任何参数。

```js
rl.on('SIGINT', () => {
  rl.question('确定要退出吗？', (answer) => {
    if (answer.match(/^y(es)?$/i)) rl.pause();
  });
});
```

