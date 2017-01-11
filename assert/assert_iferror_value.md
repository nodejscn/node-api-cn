<!-- YAML
added: v0.1.97
-->

如果 `value` 的值为真，抛出 `value`。
当测试回调函数的 `error` 参数时非常有用。

```js
const assert = require('assert');

assert.ifError(0);
// 通过
assert.ifError(1);
// 抛出 1
assert.ifError('error');
// 抛出 'error'
assert.ifError(new Error());
// 抛出 Error
```

