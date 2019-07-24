<!-- YAML
added: v0.11.5
deprecated: v4.0.0
-->

> Stability: 0 - Deprecated:
> Use `value !== null && typeof value === 'object'` instead.

* `object` {any}
* Returns: {boolean}

Returns `true` if the given `object` is strictly an `Object` **and** not a
`Function` (even though functions are objects in JavaScript).
Otherwise, returns `false`.

```js
const util = require('util');

util.isObject(5);
// Returns: false
util.isObject(null);
// Returns: false
util.isObject({});
// Returns: true
util.isObject(() => {});
// Returns: false
```

