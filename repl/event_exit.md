<!-- YAML
added: v0.7.7
-->

当收到 `.exit` 命令、用户按下两次 `<ctrl>-C` 发出 `SIGINT` 信号、或者是输入中按下 `<ctrl>-D` 发出 `'end'` 信号，都会触发 `'exit'` 事件。
监听事件的回调函数将被不带参数地触发。

```js
replServer.on('exit', () => {
  console.log('从 REPL 接收到 "exit" 事件！');
  process.exit();
});
```

