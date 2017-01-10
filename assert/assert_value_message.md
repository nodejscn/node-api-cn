<!-- YAML
added: v0.5.9
-->

An alias of [`assert.ok()`][] .

```js
const assert = require('assert');

assert(true);
// OK
assert(1);
// OK
assert(false);
// throws "AssertionError: false == true"
assert(0);
// throws "AssertionError: 0 == true"
assert(false, 'it\'s false');
// throws "AssertionError: it's false"
```

