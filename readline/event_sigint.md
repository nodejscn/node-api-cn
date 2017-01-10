<!-- YAML
added: v0.3.0
-->

The `'SIGINT'` event is emitted whenever the `input` stream receives a
`<ctrl>-C` input, known typically as `SIGINT`. If there are no `'SIGINT'` event
listeners registered when the `input` stream receives a `SIGINT`, the `'pause'`
event will be emitted.

The listener function is invoked without passing any arguments.

For example:

```js
rl.on('SIGINT', () => {
  rl.question('Are you sure you want to exit?', (answer) => {
    if (answer.match(/^y(es)?$/i)) rl.pause();
  });
});
```

