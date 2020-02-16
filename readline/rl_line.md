<!-- YAML
added: 0.1.98
-->

* {string|undefined}

The current input data being processed by node.

This can be used when collecting input from a TTY stream to retrieve the
current value that has been processed thus far, prior to the `line` event
being emitted.  Once the `line` event has been emitted, this property will
be an empty string.

Be aware that modifying the value during the instance runtime may have
unintended consequences if `rl.cursor` is not also controlled.

**If not using a TTY stream for input, use the [`'line'`][] event.**

One possible use case would be as follows:

```js
const values = ['lorem ipsum', 'dolor sit amet'];
const rl = readline.createInterface(process.stdin);
const showResults = debounce(() => {
  console.log(
    '\n',
    values.filter((val) => val.startsWith(rl.line)).join(' ')
  );
}, 300);
process.stdin.on('keypress', (c, k) => {
  showResults();
});
```

