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
原始值使用 [相等运算符]（`==`）比较。

只比较 [可枚举的自身属性]。
[`assert.deepEqual()`] 不比较对象的 [原型]、连接符、或不可枚举的属性（这些情况可以使用 [`assert.deepStrictEqual()`]）。
这可能会导致一些意料之外的结果。
例如，下面的例子不会抛出 `AssertionError`，因为 [Error](errors.html#errors_class_error) 对象的属性是不可枚举的：

```js
// 注意：这不会抛出 AssertionError！
assert.deepEqual(Error('a'), Error('b'));
```

An exception is made for [`Map`][] and [`Set`][]. Maps and Sets have their
contained items compared too, as expected.

深度相等意味着子对象的可枚举的自身属性也会被比较：

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
// 通过，对象与自身相等

assert.deepEqual(obj1, obj2);
// 抛出 AssertionError: { a: { b: 1 } } deepEqual { a: { b: 2 } }
// b 的值不同

assert.deepEqual(obj1, obj3);
// 通过，两个对象相等

assert.deepEqual(obj1, obj4);
// 抛出 AssertionError: { a: { b: 1 } } deepEqual {}
// 原型会被忽略
```

如果两个值不相等，则抛出一个带有 `message` 属性的 `AssertionError`，其中 `message` 属性的值等于传入的 `message` 参数的值。
如果 `message` 参数为 `undefined`，则赋予默认的错误信息。

