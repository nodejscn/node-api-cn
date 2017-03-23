
`Buffer` 实例可以使用 ECMAScript 2015 (ES6) 的 `for..of` 语法进行遍历。

例子：

```js
const buf = Buffer.from([1, 2, 3]);

// 输出:
//   1
//   2
//   3
for (const b of buf) {
  console.log(b);
}
```

此外，[`buf.values()`] 、[`buf.keys()`] 和 [`buf.entries()`] 方法可用于创建迭代器。

