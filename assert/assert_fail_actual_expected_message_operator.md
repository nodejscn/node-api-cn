<!-- YAML
added: v0.1.21
-->
* `actual` {any}
* `expected` {any}
* `message` {any}
* `operator` {String} (默认: '!=')

抛出 `AssertionError`。
如果 `message` 不存在，则错误信息会被设为 `actual` 的值加分隔符 `operator` 再加 `expected` 的值。
否则，错误信息为 `message` 的值。

```js
const assert = require('assert');

assert.fail(1, 2, undefined, '>');
// 抛出 AssertionError: 1 > 2

assert.fail(1, 2, '错误信息', '>');
// 抛出 AssertionError: 错误信息

assert.fail('错误信息');
// 抛出 AssertionError: 错误信息

assert.fail('a', 'b');
// 抛出 AssertionError: 'a' != 'b'
```

