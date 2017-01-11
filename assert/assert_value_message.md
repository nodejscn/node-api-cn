<!-- YAML
added: v0.5.9
-->

[`assert.ok()`](#assert_assert_ok_value_message) 的别名。

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
assert(false, 'it\'s false');
// 抛出 "AssertionError: it's false"
```

