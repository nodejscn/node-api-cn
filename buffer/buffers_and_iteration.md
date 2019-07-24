
`Buffer` 实例可以使用 `for..of` 语法进行迭代：

```js
const buf = Buffer.from([1, 2, 3]);

for (const b of buf) {
  console.log(b);
}
// 打印:
//   1
//   2
//   3
```

此外，[`buf.values()`]、[`buf.keys()`]、和 [`buf.entries()`] 方法也可用于创建迭代器。

