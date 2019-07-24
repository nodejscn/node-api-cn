<!-- YAML
added: v10.7.0
-->

* Returns: {bigint}

The `bigint` version of the [`process.hrtime()`][] method returning the
current high-resolution real time in a `bigint`.

Unlike [`process.hrtime()`][], it does not support an additional `time`
argument since the difference can just be computed directly
by subtraction of the two `bigint`s.

```js
const start = process.hrtime.bigint();
// 191051479007711n

setTimeout(() => {
  const end = process.hrtime.bigint();
  // 191052633396993n

  console.log(`Benchmark took ${end - start} nanoseconds`);
  // Benchmark took 1154389282 nanoseconds
}, 1000);
```

