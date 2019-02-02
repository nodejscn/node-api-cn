<!-- YAML
added: v0.1.97
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18247
    description: Instead of throwing the original error it is now wrapped into
                 an `AssertionError` that contains the full stack trace.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18247
    description: Value may now only be `undefined` or `null`. Before all falsy
                 values were handled the same as `null` and did not throw.
-->
* `value` {any}

如果 `value` 不为 `undefined` 或 `null`，则抛出 `value`。 
在回调中测试 `error` 参数时，这很有用。 
堆栈跟踪包含传递给 `ifError()` 的错误的所有帧，包括 `ifError()` 本身的潜在新帧。

```js
const assert = require('assert').strict;

assert.ifError(null);
// 通过。
assert.ifError(0);
// AssertionError [ERR_ASSERTION]: ifError got unwanted exception: 0
assert.ifError('错误');
// AssertionError [ERR_ASSERTION]: ifError got unwanted exception: '错误'
assert.ifError(new Error());
// AssertionError [ERR_ASSERTION]: ifError got unwanted exception: Error

// 创建一些随机错误帧。
let err;
(function errorFrame() {
  err = new Error('测试错误');
})();

(function ifErrorFrame() {
  assert.ifError(err);
})();
// AssertionError [ERR_ASSERTION]: ifError got unwanted exception: 测试错误
//     at ifErrorFrame
//     at errorFrame
```

