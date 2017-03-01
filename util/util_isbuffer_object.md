<!-- YAML
added: v0.11.5
deprecated: v4.0.0
-->

> 稳定性: 0 - 废弃的: 使用 [`Buffer.isBuffer()`] 代替。

* `object` {any}

Returns `true` if the given `object` is a `Buffer`. Otherwise, returns `false`.

```js
const util = require('util');

util.isBuffer({ length: 0 });
// Returns: false
util.isBuffer([]);
// Returns: false
util.isBuffer(Buffer.from('hello world'));
// Returns: true
```

