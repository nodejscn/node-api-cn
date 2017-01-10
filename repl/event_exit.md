<!-- YAML
added: v0.7.7
-->

The `'exit'` event is emitted when the REPL is exited either by receiving the
`.exit` command as input, the user pressing `<ctrl>-C` twice to signal `SIGINT`,
or by pressing `<ctrl>-D` to signal `'end'` on the input stream. The listener
callback is invoked without any arguments.

```js
replServer.on('exit', () => {
  console.log('Received "exit" event from repl!');
  process.exit();
});
```

