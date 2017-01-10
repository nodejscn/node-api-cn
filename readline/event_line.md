<!-- YAML
added: v0.1.98
-->

The `'line'` event is emitted whenever the `input` stream receives an
end-of-line input (`\n`, `\r`, or `\r\n`). This usually occurs when the user
presses the `<Enter>`, or `<Return>` keys.

The listener function is called with a string containing the single line of
received input.

For example:

```js
rl.on('line', (input) => {
  console.log(`Received: ${input}`);
});
```

