
> Stability: 0 - Deprecated: Use strict mode instead.

When accessing `assert` directly instead of using the `strict` property, the
[Abstract Equality Comparison][] will be used for any function without "strict"
in its name, such as [`assert.deepEqual()`][].

It can be accessed using:

```js
const assert = require('assert');
```

It is recommended to use the [`strict mode`][] instead as the
[Abstract Equality Comparison][] can often have surprising results. This is
especially true for [`assert.deepEqual()`][], where the comparison rules are
lax:

```js
// WARNING: This does not throw an AssertionError!
assert.deepEqual(/a/gi, new Date());
```

