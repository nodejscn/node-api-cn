
* 使用 [SameValue比较][SameValue Comparison]（使用 [`Object.is()`]）来比较原始值。
* 对象的[类型标签][Object.prototype.toString()]应该相同。
* 使用[严格相等比较][Strict Equality Comparison]来比较对象的[原型][prototype-spec]。
* 只考虑[可枚举的自身属性][enumerable "own" properties]。
* 始终比较 [`Error`] 的名称和消息，即使这些不是可枚举的属性。
* 可枚举的自身 [`Symbol`] 属性也会比较。
* [对象封装器][Object wrappers]作为对象和解封装后的值都进行比较。
* `Object` 属性的比较是无序的。
* `Map` 键名与 `Set` 子项的比较是无序的。
* 当两边的值不相同或遇到循环引用时，递归停止。
* [`WeakMap`] 和 [`WeakSet`] 的比较不依赖于它们的值。请参阅下文了解更多详情。

```js
const assert = require('assert').strict;

// 失败，因为 1 !== '1'。
assert.deepStrictEqual({ a: 1 }, { a: '1' });
// AssertionError: Input A expected to strictly deep-equal input B:
// + expected - actual
//   {
// -   a: 1
// +   a: '1'
//   }

// 以下对象没有自身属性。
const date = new Date();
const object = {};
const fakeDate = {};
Object.setPrototypeOf(fakeDate, Date.prototype);

// 原型不同：
assert.deepStrictEqual(object, fakeDate);
// AssertionError: Input A expected to strictly deep-equal input B:
// + expected - actual
// - {}
// + Date {}

// 类型标签不同：
assert.deepStrictEqual(date, fakeDate);
// AssertionError: Input A expected to strictly deep-equal input B:
// + expected - actual
// - 2018-04-26T00:49:08.604Z
// + Date {}

assert.deepStrictEqual(NaN, NaN);
// 通过，因为使用 SameValue 比较。

// 解封装后的数字不同：
assert.deepStrictEqual(new Number(1), new Number(2));
// AssertionError: Input A expected to strictly deep-equal input B:
// + expected - actual
// - [Number: 1]
// + [Number: 2]

assert.deepStrictEqual(new String('foo'), Object('foo'));
// 通过，因为对象与解封装后的字符串都是相同的。

assert.deepStrictEqual(-0, -0);
// 通过。

// 使用 SameValue 比较的零不同：
assert.deepStrictEqual(0, -0);
// AssertionError: Input A expected to strictly deep-equal input B:
// + expected - actual
// - 0
// + -0

const symbol1 = Symbol();
const symbol2 = Symbol();
assert.deepStrictEqual({ [symbol1]: 1 }, { [symbol1]: 1 });
// 通过，因为在两个对象上的 symbol 相同。
assert.deepStrictEqual({ [symbol1]: 1 }, { [symbol2]: 1 });
// AssertionError [ERR_ASSERTION]: Input objects not identical:
// {
//   [Symbol()]: 1
// }

const weakMap1 = new WeakMap();
const weakMap2 = new WeakMap([[{}, {}]]);
const weakMap3 = new WeakMap();
weakMap3.unequal = true;

assert.deepStrictEqual(weakMap1, weakMap2);
// 通过，因为无法比较条目。

// 失败，因为 weakMap3 有一个 weakMap1 不包含的属性：
assert.deepStrictEqual(weakMap1, weakMap3);
// AssertionError: Input A expected to strictly deep-equal input B:
// + expected - actual
//   WeakMap {
// -   [items unknown]
// +   [items unknown],
// +   unequal: true
//   }
```

如果值不相等，则抛出 `AssertionError`，并将 `message` 属性设置为等于 `message` 参数的值。
如果未定义 `message` 参数，则会分配默认错误消息。
如果 `message` 参数是 [`Error`] 的实例，那么它将被抛出而不是 `AssertionError`。

