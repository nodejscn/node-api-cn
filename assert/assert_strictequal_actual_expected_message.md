<!-- YAML
added: v0.1.21
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17003
    description: Used comparison changed from Strict Equality to `Object.is()`
-->
* `actual` {any}
* `expected` {any}
* `message` {string|Error}

使用 [SameValue比较法][SameValue Comparison]测试 `actual` 与 `expected` 是否全等。

```js
const assert = require('assert').strict;

assert.strictEqual(1, 2);
// 抛出 AssertionError [ERR_ASSERTION]: Input A expected to strictly equal input B:
// + expected - actual
// - 1
// + 2

assert.strictEqual(1, 1);
// 测试通过。

assert.strictEqual(1, '1');
// 抛出 AssertionError [ERR_ASSERTION]: Input A expected to strictly equal input B:
// + expected - actual
// - 1
// + '1'
```

如果两个值不全等，则抛出 `AssertionError`。

