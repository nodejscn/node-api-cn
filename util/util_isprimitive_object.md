<!-- YAML
added: v0.11.5
deprecated: v4.0.0
-->

> Stability: 0 - Deprecated: Use
> `(typeof value !== 'object' && typeof value !== 'function') || value === null`
> instead.

* `object` {any}
* Returns: {boolean}

Returns `true` if the given `object` is a primitive type. Otherwise, returns
`false`.

```js
const util = require('util');

util.isPrimitive(5);
// Returns: true
util.isPrimitive('foo');
// Returns: true
util.isPrimitive(false);
// Returns: true
util.isPrimitive(null);
// Returns: true
util.isPrimitive(undefined);
// Returns: true
util.isPrimitive({});
// Returns: false
util.isPrimitive(() => {});
// Returns: false
util.isPrimitive(/^$/);
// Returns: false
util.isPrimitive(new Date());
// Returns: false
```

