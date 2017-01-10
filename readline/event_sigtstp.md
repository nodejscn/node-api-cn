<!-- YAML
added: v0.7.5
-->

The `'SIGTSTP'` event is emitted when the `input` stream receives a `<ctrl>-Z`
input, typically known as `SIGTSTP`. If there are no `SIGTSTP` event listeners
registered when the `input` stream receives a `SIGTSTP`, the Node.js process
will be sent to the background.

When the program is resumed using fg(1), the `'pause'` and `SIGCONT` events
will be emitted. These can be used to resume the `input` stream.

The `'pause'` and `'SIGCONT'` events will not be emitted if the `input` was
paused before the process was sent to the background.

The listener function is invoked without passing any arguments.

For example:

```js
rl.on('SIGTSTP', () => {
  // This will override SIGTSTP and prevent the program from going to the
  // background.
  console.log('Caught SIGTSTP.');
});
```

*Note*: The `'SIGTSTP'` event is _not_ supported on Windows.

