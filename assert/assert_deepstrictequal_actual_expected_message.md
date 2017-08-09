<!-- YAML
added: v1.2.0
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12142
    description: Set and Map content is also compared
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
* `message` {any}

大多数情况下与 `assert.deepEqual()` 一样，但有三个例外：

1. 原始值使用 [全等运算符]（`===`）比较。使用[SameValueZero][]比较法来比较设置的值及映射的键（也就意味不用考虑[caveats][]）。
2. 对象的 [原型] 也使用 [全等运算符] 比较。
3. 对象的[类型标签][Object.prototype.toString()]应该相同。

```js
const assert = require('assert');

assert.deepEqual({ a: 1 }, { a: '1' });
// 通过，因为 1 == '1'

assert.deepStrictEqual({ a: 1 }, { a: '1' });
// 抛出 AssertionError: { a: 1 } deepStrictEqual { a: '1' }
// 因为使用全等运算符 1 !== '1' 

// 以下对象没有自己的属性
const date = new Date();
const object = {};
const fakeDate = {};

Object.setPrototypeOf(fakeDate, Date.prototype);

assert.deepEqual(object, fakeDate);
// 通过，不检查原型[[Prototype]]
assert.deepStrictEqual(object, fakeDate);
// 抛出 AssertionError: {} deepStrictEqual Date {}
// 因为原型 [[Prototype]] 不同

assert.deepEqual(date, fakeDate);
// 通过，不检查类型标签
assert.deepStrictEqual(date, fakeDate);
// 抛出 AssertionError: 2017-03-11T14:25:31.849Z deepStrictEqual Date {}
// 因为类型标签不同
```

如果两个值不相等，则抛出一个带有 `message` 属性的 `AssertionError`，其中 `message` 属性的值等于传入的 `message` 参数的值。
如果 `message` 参数为 `undefined`，则赋予默认的错误信息。

