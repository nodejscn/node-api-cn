<!-- YAML
added: v0.7.7
-->

* `stream` {Readable}
* `interface` {readline.Interface}

The `readline.emitKeypressEvents()` method causes the given [Writable][]
`stream` to begin emitting `'keypress'` events corresponding to received input.

Optionally, `interface` specifies a `readline.Interface` instance for which
autocompletion is disabled when copy-pasted input is detected.

If the `stream` is a [TTY][], then it must be in raw mode.

```js
readline.emitKeypressEvents(process.stdin);
if (process.stdin.isTTY)
  process.stdin.setRawMode(true);
```

