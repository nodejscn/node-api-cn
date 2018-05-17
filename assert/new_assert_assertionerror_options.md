<!-- YAML
added: v0.1.21
-->
* `options` {Object}
  * `message` {string} If provided, the error message is going to be set to this
    value.
  * `actual` {any} The `actual` property on the error instance is going to
    contain this value. Internally used for the `actual` error input in case
    e.g., [`assert.strictEqual()`] is used.
  * `expected` {any} The `expected` property on the error instance is going to
    contain this value. Internally used for the `expected` error input in case
    e.g., [`assert.strictEqual()`] is used.
  * `operator` {string} The `operator` property on the error instance is going
    to contain this value. Internally used to indicate what operation was used
    for comparison (or what assertion function triggered the error).
  * `stackStartFn` {Function} If provided, the generated stack trace is going to
    remove all frames up to the provided function.

A subclass of `Error` that indicates the failure of an assertion.

All instances contain the built-in `Error` properties (`message` and `name`)
and:

* `actual` {any} Set to the actual value in case e.g.,
  [`assert.strictEqual()`] is used.
* `expected` {any} Set to the expected value in case e.g.,
  [`assert.strictEqual()`] is used.
* `generatedMessage` {boolean} Indicates if the message was auto-generated
  (`true`) or not.
* `code` {string} This is always set to the string `ERR_ASSERTION` to indicate
  that the error is actually an assertion error.
* `operator` {string} Set to the passed in operator value.

```js
const assert = require('assert');

// Generate an AssertionError to compare the error message later:
const { message } = new assert.AssertionError({
  actual: 1,
  expected: 2,
  operator: 'strictEqual'
});

// Verify error output:
try {
  assert.strictEqual(1, 2);
} catch (err) {
  assert(err instanceof assert.AssertionError);
  assert.strictEqual(err.message, message);
  assert.strictEqual(err.name, 'AssertionError [ERR_ASSERTION]');
  assert.strictEqual(err.actual, 1);
  assert.strictEqual(err.expected, 2);
  assert.strictEqual(err.code, 'ERR_ASSERTION');
  assert.strictEqual(err.operator, 'strictEqual');
  assert.strictEqual(err.generatedMessage, true);
}
```

