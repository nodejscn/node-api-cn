<!-- YAML
added: v1.1.0
-->

* 返回: {Iterator}

创建并返回 `buf` 键值（字节）的[迭代器][iterator]。
当对 `Buffer` 使用 `for..of` 时会调用该函数。

```js
const buf = Buffer.from('buffer');

for (const value of buf.values()) {
  console.log(value);
}
// 打印:
//   98
//   117
//   102
//   102
//   101
//   114

for (const value of buf) {
  console.log(value);
}
// 打印:
//   98
//   117
//   102
//   102
//   101
//   114
```

