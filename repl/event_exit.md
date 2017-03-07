<!-- YAML
added: v0.7.7
-->

The `'exit'` event is emitted when the REPL is exited either by receiving the
`.exit` command as input, the user pressing `<ctrl>-C` twice to signal `SIGINT`,
or by pressing `<ctrl>-D` to signal `'end'` on the input stream. The listener
callback is invoked without any arguments.
当收到`.exit`命令、用户按下两次`<ctrl>-C`发出 `SIGINT`信号、或者是输入中按下`<ctrl>-D`发出`'end'`信号，都会触发`'exit'`事件。
监听事件的回调函数将被不带参数地触发。


```js
replServer.on('exit', () => {
  console.log('Received "exit" event from repl!');
  process.exit();
});
```

