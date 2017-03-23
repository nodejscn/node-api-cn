<!-- YAML
added: v1.1.0
-->

* 返回: {Iterator}

从 `buf` 的内容中，创建并返回一个 `[index, byte]` 形式的[迭代器]。

例子：记录一个 `Buffer` 全部的内容。

```js
const buf = Buffer.from('buffer');

// 输出:
//   [0, 98]
//   [1, 117]
//   [2, 102]
//   [3, 102]
//   [4, 101]
//   [5, 114]
for (const pair of buf.entries()) {
  console.log(pair);
}
```

