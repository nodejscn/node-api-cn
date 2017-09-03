<!-- YAML
added: v0.1.21
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12142
    description: Set and Map content is also compared
  - version: v6.4.0, v4.7.1
    pr-url: https://github.com/nodejs/node/pull/8002
    description: Typed array slices are handled correctly now.
  - version: v6.1.0, v4.5.0
    pr-url: https://github.com/nodejs/node/pull/6432
    description: Objects with circular references can be used as inputs now.
  - version: v5.10.1, v4.4.3
    pr-url: https://github.com/nodejs/node/pull/5910
    description: Handle non-`Uint8Array` typed arrays correctly.
-->
* `actual` {any}
* `expected` {any}
* `message` {any}

测试 `actual` 参数与 `expected` 参数是否深度相等。
原始值使用[相等运算符]（`==`）比较。

只测试[可枚举的自身属性]，不测试对象的[原型]、连接符、或不可枚举的属性（这些情况使用 [`assert.deepStrictEqual()`]）。
例如，下面的例子不会抛出 `AssertionError`，因为 [`Error`] 对象的属性不是可枚举的：

```js
// 不会抛出 AssertionError。
assert.deepEqual(Error('a'), Error('b'));
```

[`Map`] 和 [`Set`] 包含的子项也会被测试。

子对象中可枚举的自身属性也会被测试：

```js
const assert = require('assert');

const obj1 = {
  a: {
    b: 1
  }
};
const obj2 = {
  a: {
    b: 2
  }
};
const obj3 = {
  a: {
    b: 1
  }
};
const obj4 = Object.create(obj1);

assert.deepEqual(obj1, obj1);
// 测试通过，对象与自身相等。

assert.deepEqual(obj1, obj2);
// 抛出 AssertionError: { a: { b: 1 } } deepEqual { a: { b: 2 } }
// 因为 b 属性的值不同。

assert.deepEqual(obj1, obj3);
// 测试通过，两个对象相等。

assert.deepEqual(obj1, obj4);
// 抛出 AssertionError: { a: { b: 1 } } deepEqual {}
// 因为不测试原型。
```

如果两个值不相等，则抛出一个带有 `message` 属性的 `AssertionError`，其中 `message` 属性的值等于传入的 `message` 参数的值。
如果 `message` 参数为 `undefined`，则赋予默认的错误信息。

