<!-- YAML
added: v0.5.9
-->

[`assert.ok()`] 的别名。

```js
const assert = require('assert');

assert(true);
// 通过
assert(1);
// 通过
assert(false);
// 抛出 "AssertionError: false == true"
assert(0);
// 抛出 "AssertionError: 0 == true"
assert(false, '不是真值');
// 抛出 "AssertionError: 不是真值"
```

