<!-- YAML
added: v1.2.0
-->

Generally identical to `assert.deepEqual()` with two exceptions. First,
primitive values are compared using the strict equality operator ( `===` ).
Second, object comparisons include a strict equality check of their prototypes.

```js
const assert = require('assert');

assert.deepEqual({a:1}, {a:'1'});
// OK, because 1 == '1'

assert.deepStrictEqual({a:1}, {a:'1'});
// AssertionError: { a: 1 } deepStrictEqual { a: '1' }
// because 1 !== '1' using strict equality
```

If the values are not equal, an `AssertionError` is thrown with a `message`
property set equal to the value of the `message` parameter. If the `message`
parameter is undefined, a default error message is assigned.

