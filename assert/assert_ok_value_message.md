<!-- YAML
added: v0.1.21
-->

测试 `value` 是否为真值。
相当于 `assert.equal(!!value, true, message)`。

如果 `value` 不为真值，则抛出一个带有 `message` 属性的 `AssertionError`，其中 `message` 属性的值等于传入的 `message` 参数的值。
如果 `message` 参数为 `undefined`，则输出默认的错误信息。

```js
const assert = require('assert');

assert.ok(true);
// 通过
assert.ok(1);
// 通过
assert.ok(false);
// 抛出 "AssertionError: false == true"
assert.ok(0);
// 抛出 "AssertionError: 0 == true"
assert.ok(false, 'it\'s false');
// 抛出 "AssertionError: it's false"
```

