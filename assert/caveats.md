
对于 [SameValueZero] 比较，建议使用 ES2015 的 [`Object.is()`]。

```js
const a = 0;
const b = -a;
assert.notStrictEqual(a, b);
// 抛出 AssertionError: 0 !== -0
// 因为全等运算符不区分 -0 与 +0。
assert(!Object.is(a, b));
// 但 Object.is() 可以区分。

const str1 = 'foo';
const str2 = 'foo';
assert.strictEqual(str1 / 1, str2 / 1);
// 抛出 AssertionError: NaN === NaN
// 因为全等运算符不能用于测试 NaN。
assert(Object.is(str1 / 1, str2 / 1));
// 但 Object.is() 可以测试。
```

详见[MDN的等式比较指南]。

