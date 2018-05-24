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
可用于测试回调函数的 `error` 参数。
堆栈踪迹会包含传入 `ifError()` 的错误的所有帧，包括潜在的 `ifError()` 自身新增的帧。

例子：

```js
const assert = require('assert').strict;

assert.ifError(null);
// 通过。
assert.ifError(0);
// 抛出 AssertionError [ERR_ASSERTION]: ifError got unwanted exception: 0
assert.ifError('错误信息');
// 抛出 AssertionError [ERR_ASSERTION]: ifError got unwanted exception: '错误信息'
assert.ifError(new Error());
// 抛出 AssertionError [ERR_ASSERTION]: ifError got unwanted exception: Error

// 添加一些错误帧。
let err;
(function errorFrame() {
  err = new Error('错误信息');
})();

(function ifErrorFrame() {
  assert.ifError(err);
})();
// AssertionError [ERR_ASSERTION]: ifError got unwanted exception: 错误信息
//     at ifErrorFrame
//     at errorFrame
```

