
对于以下情况，如使用 [SameValueZero][] 作比较， 请优先考虑使用 ES2015 的 [`Object.is()`][]

```js
const a = 0;
const b = -a;
assert.notStrictEqual(a, b);
// 断言错误: 0 !== -0
// 不全等比较方法 不能区分 -0 和 +0 的差异
assert(!Object.is(a, b));
// 但 Object.is() 可以

const str1 = 'foo';
const str2 = 'foo';
assert.strictEqual(str1 / 1, str2 / 1);
// 断言错误: NaN === NaN
// 不全等比较方法 不能用来检查 NaN
assert(Object.is(str1 / 1, str2 / 1));
// 但 Object.is() 可以
```

你可以访问 [MDN's guide on equality comparisons and sameness][mdn-equality-guide] 以便获取更多信息

