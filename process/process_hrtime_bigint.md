<!-- YAML
added: v10.7.0
-->

* 返回: {bigint}

[`process.hrtime()`] 方法的 `bigint` 版本，返回当前的高精度实际时间（以纳秒为单位的 `bigint` 型）。

与 [`process.hrtime()`] 不同，它不支持额外的 `time` 参数，因为可以直接通过两个 `bigint` 相减来计算差异。

```js
const start = process.hrtime.bigint();
// 191051479007711n

setTimeout(() => {
  const end = process.hrtime.bigint();
  // 191052633396993n

  console.log(`基准测试耗时 ${end - start} 纳秒`);
  // 基准测试耗时 1154389282 纳秒
}, 1000);
```

