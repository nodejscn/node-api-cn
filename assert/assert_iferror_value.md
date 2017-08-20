<!-- YAML
added: v0.1.97
-->
* `value` {any}

如果 `value` 为真，则抛出 `value`。
可用于测试回调函数的 `error` 参数。

```js
const assert = require('assert');

assert.ifError(0);
// 测试通过。
assert.ifError(1);
// 抛出 1。
assert.ifError('error');
// 抛出 'error'。
assert.ifError(new Error());
// 抛出 Error。
```

