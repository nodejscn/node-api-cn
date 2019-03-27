<!-- YAML
added: v1.1.0
-->

* 返回: {Iterator}

创建并返回 `buf` 键名（索引）的[迭代器][iterator]。

```js
const buf = Buffer.from('buffer');

for (const key of buf.keys()) {
  console.log(key);
}
// 打印:
//   0
//   1
//   2
//   3
//   4
//   5
```

