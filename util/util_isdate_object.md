<!-- YAML
added: v0.6.0
deprecated: v4.0.0
-->

> 稳定性: 0 - 废弃的

* `object` {any}

Returns `true` if the given `object` is a `Date`. Otherwise, returns `false`.

```js
const util = require('util');

util.isDate(new Date());
// Returns: true
util.isDate(Date());
// false (without 'new' returns a String)
util.isDate({});
// Returns: false
```

