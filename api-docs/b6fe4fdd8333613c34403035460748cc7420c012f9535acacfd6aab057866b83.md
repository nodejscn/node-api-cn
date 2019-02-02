<!-- YAML
added: v1.2.0
changes:
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15398
    description: The `-0` and `+0` are not considered equal anymore.
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15036
    description: The `NaN` is now compared using the
              [SameValueZero](https://tc39.github.io/ecma262/#sec-samevaluezero)
              comparison.
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15001
    description: The `Error` names and messages are now properly compared
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12142
    description: The `Set` and `Map` content is also compared
  - version: v6.4.0, v4.7.1
    pr-url: https://github.com/nodejs/node/pull/8002
    description: Typed array slices are handled correctly now.
  - version: v6.1.0
    pr-url: https://github.com/nodejs/node/pull/6432
    description: Objects with circular references can be used as inputs now.
  - version: v5.10.1, v4.4.3
    pr-url: https://github.com/nodejs/node/pull/5910
    description: Handle non-`Uint8Array` typed arrays correctly.
-->
* `actual` {any}
* `expected` {any}
* `message` {string|Error}

测试深度严格的不平等。 
与 [`assert.deepStrictEqual()`] 相反。

```js
const assert = require('assert').strict;

assert.notDeepStrictEqual({ a: 1 }, { a: '1' });
// 通过。
```

如果值深度且严格相等，则抛出 `AssertionError`，并将 `message` 属性设置为等于 `message` 参数的值。 
如果未定义 `message` 参数，则会分配默认错误消息。 
如果 `message` 参数是 [`Error`] 的实例，则它将被抛出而不是 `AssertionError`。

