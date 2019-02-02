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

测试 `actual` 参数和 `expected` 参数之间的严格不相等，使用 [SameValue比较][SameValue Comparison]。

```js
const assert = require('assert').strict;

assert.notStrictEqual(1, 2);
// 通过。

assert.notStrictEqual(1, 1);
// AssertionError [ERR_ASSERTION]: Identical input passed to notStrictEqual: 1

assert.notStrictEqual(1, '1');
// 通过。
```

如果值严格相等，则抛出 `AssertionError`，并将 `message` 属性设置为等于 `message` 参数的值。 
如果未定义 `message` 参数，则会分配默认错误消息。 
如果 `message` 参数是 [`Error`] 的实例，则它将被抛出而不是 `AssertionError`。


