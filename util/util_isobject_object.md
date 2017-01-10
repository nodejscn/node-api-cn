<!-- YAML
added: v0.11.5
deprecated: v4.0.0
-->

> Stability: 0 - Deprecated

* `object` {any}

Returns `true` if the given `object` is strictly an `Object` **and** not a
`Function`. Otherwise, returns `false`.

```js
const util = require('util');

util.isObject(5);
// Returns: false
util.isObject(null);
// Returns: false
util.isObject({});
// Returns: true
util.isObject(function(){});
// Returns: false
```

