<!-- YAML
added: v0.7.5
-->

The `'SIGCONT'` event is emitted when a Node.js process previously moved into
the background using `<ctrl>-Z` (i.e. `SIGTSTP`) is then brought back to the
foreground using fg(1).

If the `input` stream was paused *before* the `SIGTSTP` request, this event will
not be emitted.

The listener function is invoked without passing any arguments.

For example:

```js
rl.on('SIGCONT', () => {
  // `prompt` will automatically resume the stream
  rl.prompt();
});
```

*Note*: The `'SIGCONT'` event is _not_ supported on Windows.

