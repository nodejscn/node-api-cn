<!-- YAML
added: v0.3.3
-->

* `query` {String} A statement or query to write to `output`, prepended to the
  prompt.
* `callback` {Function} A callback function that is invoked with the user's
  input in response to the `query`.

The `rl.question()` method displays the `query` by writing it to the `output`,
waits for user input to be provided on `input`, then invokes the `callback`
function passing the provided input as the first argument.

When called, `rl.question()` will resume the `input` stream if it has been
paused.

If the `readline.Interface` was created with `output` set to `null` or
`undefined` the `query` is not written.

Example usage:

```js
rl.question('What is your favorite food?', (answer) => {
  console.log(`Oh, so your favorite food is ${answer}`);
});
```

*Note*: The `callback` function passed to `rl.question()` does not follow the
typical pattern of accepting an `Error` object or `null` as the first argument.
The `callback` is called with the provided answer as the only argument.

