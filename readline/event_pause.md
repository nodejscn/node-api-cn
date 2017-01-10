<!-- YAML
added: v0.7.5
-->

The `'pause'` event is emitted when one of the following occur:

* The `input` stream is paused.
* The `input` stream is not paused and receives the `SIGCONT` event. (See
  events [`SIGTSTP`][] and [`SIGCONT`][])

The listener function is called without passing any arguments.

For example:

```js
rl.on('pause', () => {
  console.log('Readline paused.');
});
```

