
`Buffer` 实例可以通过 `for..of` 语法进行迭代:

```js
const buf = Buffer.from([1, 2, 3]);

// 打印:
//   1
//   2
//   3
for (const b of buf) {
  console.log(b);
}
```

此外, 可以通过 [`buf.values()`], [`buf.keys()`], 和
[`buf.entries()`] 方法来创建iterators.

