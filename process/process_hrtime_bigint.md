<!-- YAML
added: v10.7.0
-->

* 返回: {bigint}

[`process.hrtime()`] 方法的 `bigint` 版本在 `bigint` 中返回当前的高精度实时。

与 [`process.hrtime()`] 不同，它不支持额外的 `time` 参数，因为差异可以直接通过减去两个 `bigint` 来计算。

```js
const start = process.hrtime.bigint();
// 191051479007711n

setTimeout(() => {
  const end = process.hrtime.bigint();
  // 191052633396993n

  console.log(`基准工具 ${end - start} 纳秒`);
  // 基准工具 1154389282 纳秒
}, 1000);
```

