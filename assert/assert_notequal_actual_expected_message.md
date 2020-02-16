<!-- YAML
added: v0.1.21
-->

* `actual` {any}
* `expected` {any}
* `message` {string|Error}

**Strict mode**

An alias of [`assert.notStrictEqual()`][].

**Legacy mode**

> Stability: 0 - Deprecated: Use [`assert.notStrictEqual()`][] instead.

Tests shallow, coercive inequality with the [Abstract Equality Comparison][]
( `!=` ).

```js
const assert = require('assert');

assert.notEqual(1, 2);
// OK

assert.notEqual(1, 1);
// AssertionError: 1 != 1

assert.notEqual(1, '1');
// AssertionError: 1 != '1'
```

If the values are equal, an [`AssertionError`][] is thrown with a `message`
property set equal to the value of the `message` parameter. If the `message`
parameter is undefined, a default error message is assigned. If the `message`
parameter is an instance of an [`Error`][] then it will be thrown instead of the
`AssertionError`.

