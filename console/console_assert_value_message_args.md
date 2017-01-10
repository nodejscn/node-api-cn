<!-- YAML
added: v0.1.101
-->

A simple assertion test that verifies whether `value` is truthy. If it is not,
an `AssertionError` is thrown. If provided, the error `message` is formatted
using [`util.format()`][] and used as the error message.

```js
console.assert(true, 'does nothing');
// OK
console.assert(false, 'Whoops %s', 'didn\'t work');
// AssertionError: Whoops didn't work
```

*Note: the `console.assert()` method is implemented differently in Node.js
than the `console.assert()` method [available in browsers][web-api-assert].*

Specifically, in browsers, calling `console.assert()` with a falsy
assertion will cause the `message` to be printed to the console without
interrupting execution of subsequent code. In Node.js, however, a falsy
assertion will cause an `AssertionError` to be thrown.

Functionality approximating that implemented by browsers can be implemented
by extending Node.js' `console` and overriding the `console.assert()` method.

In the following example, a simple module is created that extends and overrides
the default behavior of `console` in Node.js.

```js
'use strict';

// Creates a simple extension of console with a
// new impl for assert without monkey-patching.
const myConsole = Object.setPrototypeOf({
  assert(assertion, message, ...args) {
    try {
      console.assert(assertion, message, ...args);
    } catch (err) {
      console.error(err.stack);
    }
  }
}, console);

module.exports = myConsole;
```

This can then be used as a direct replacement for the built in console:

```js
const console = require('./myConsole');
console.assert(false, 'this message will print, but no error thrown');
console.log('this will also print');
```

