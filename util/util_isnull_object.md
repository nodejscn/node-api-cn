<!-- YAML
added: v0.11.5
deprecated: v4.0.0
-->

> 稳定性: 0 - 废弃的

* `object` {any}

Returns `true` if the given `object` is strictly `null`. Otherwise, returns
`false`.

```js
const util = require('util');

util.isNull(0);
// Returns: false
util.isNull(undefined);
// Returns: false
util.isNull(null);
// Returns: true
```

