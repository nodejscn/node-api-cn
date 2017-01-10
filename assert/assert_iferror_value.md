<!-- YAML
added: v0.1.97
-->

Throws `value` if `value` is truthy. This is useful when testing the `error`
argument in callbacks.

```js
const assert = require('assert');

assert.ifError(0);
// OK
assert.ifError(1);
// Throws 1
assert.ifError('error');
// Throws 'error'
assert.ifError(new Error());
// Throws Error
```

