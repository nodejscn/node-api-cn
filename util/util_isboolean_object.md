<!-- YAML
added: v0.11.5
deprecated: v4.0.0
-->

> Stability: 0 - Deprecated: Use `typeof value === 'boolean'` instead.

* `object` {any}
* Returns: {boolean}

Returns `true` if the given `object` is a `Boolean`. Otherwise, returns `false`.

```js
const util = require('util');

util.isBoolean(1);
// Returns: false
util.isBoolean(0);
// Returns: false
util.isBoolean(false);
// Returns: true
```

