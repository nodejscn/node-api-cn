<!-- YAML
added: v0.6.0
deprecated: v4.0.0
-->

> 稳定性: 0 - 废弃的

* `object` {any}

Returns `true` if the given `object` is a `RegExp`. Otherwise, returns `false`.

```js
const util = require('util');

util.isRegExp(/some regexp/);
// Returns: true
util.isRegExp(new RegExp('another regexp'));
// Returns: true
util.isRegExp({});
// Returns: false
```

