
* 使用[抽象的相等性比较][Abstract Equality Comparison]来比较原始值。
* 对象的[类型标签][Object.prototype.toString()]应该相同。
* 只考虑[可枚举的自身属性][enumerable "own" properties]。
* 始终比较 [`Error`] 的名称和消息，即使这些不是可枚举的属性。
* [对象封装器][Object wrappers]作为对象和解封装后的值都进行比较。
* `Object` 属性的比较是无序的。
* [`Map`] 键名与 [`Set`] 子项的比较是无序的。
* 当两边的值不相同或遇到循环引用时，递归停止。
* 不测试对象的 [`[[Prototype]]`][prototype-spec]。
* 可枚举的自身 [`Symbol`] 属性也会比较。
* [`WeakMap`] 和 [`WeakSet`] 的比较不依赖于它们的值。

以下示例不会抛出 `AssertionError`，因为[抽象的相等性比较][Abstract Equality Comparison]（`==`）会将原始类型视为相等。

```js
// 不会抛出 AssertionError。
assert.deepEqual('+00000000', false);
```

“深度”相等意味着还会比较子对象的可枚举“自有”属性：

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
// OK

// b 的值不同：
assert.deepEqual(obj1, obj2);
// 抛出 AssertionError: { a: { b: 1 } } deepEqual { a: { b: 2 } }

assert.deepEqual(obj1, obj3);
// OK

// 原型会被忽略：
assert.deepEqual(obj1, obj4);
// 抛出 AssertionError: { a: { b: 1 } } deepEqual {}
```

如果值不相等，则抛出 `AssertionError`，并将 `message` 属性设置为等于 `message` 参数的值。
如果未定义 `message` 参数，则会分配默认错误消息。
如果 `message` 参数是 [`Error`] 的实例，那么它将被抛出而不是 `AssertionError`。

