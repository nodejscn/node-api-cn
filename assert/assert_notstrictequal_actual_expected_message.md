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

使用 [SameValue比较法]测试 `actual` 参数与 `expected` 参数是否不全等。

```js
const assert = require('assert').strict;

assert.notStrictEqual(1, 2);
// 测试通过。

assert.notStrictEqual(1, 1);
// 抛出 AssertionError [ERR_ASSERTION]: Identical input passed to notStrictEqual: 1

assert.notStrictEqual(1, '1');
// 测试通过。
```

如果两个值全等，则抛出一个带有 `message` 属性的 `AssertionError`，其中 `message` 属性的值等于传入的 `message` 参数的值。
如果 `message` 参数为 `undefined`，则赋予默认的错误信息。
如果 `message` 参数是 [`Error`] 的实例，则会抛出它而不是 `AssertionError`。

