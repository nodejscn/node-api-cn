<!-- YAML
added: v1.1.0
-->

* 返回: {Iterator}

创建并返回一个包含 `buf` 键名（索引）的[迭代器]。

例子：

```js
const buf = Buffer.from('buffer');

// 输出:
//   0
//   1
//   2
//   3
//   4
//   5
for (const key of buf.keys()) {
  console.log(key);
}
```

