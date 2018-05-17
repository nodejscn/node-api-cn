<!-- YAML
added: v0.1.101
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17706
    description: The implementation is now spec compliant and does not throw
                 anymore.
-->
* `value` {any} The value tested for being truthy.
* `...message` {any} All arguments besides `value` are used as error message.

A simple assertion test that verifies whether `value` is truthy. If it is not,
`Assertion failed` is logged. If provided, the error `message` is formatted
using [`util.format()`][] by passing along all message arguments. The output is
used as the error message.

```js
console.assert(true, 'does nothing');
// OK
console.assert(false, 'Whoops %s work', 'didn\'t');
// Assertion failed: Whoops didn't work
```

Calling `console.assert()` with a falsy assertion will only cause the `message`
to be printed to the console without interrupting execution of subsequent code.

