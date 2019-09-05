<!-- YAML
added: v0.7.6
-->

* `time` {integer[]} 上一次调用 `process.hrtime()` 的结果。
* 返回: {integer[]}

这是在 JavaScript 中引入 `bigint` 之前的 [`process.hrtime.bigint()`] 的遗留版本。

`process.hrtime()` 方法返回当前时间以 `[seconds, nanoseconds]` 元数组表示的高精度解析值，其中 `nanoseconds` 是当前时间无法使用秒的精度表示的剩余部分。

`time` 是可选参数，传入的值是上一次调用 `process.hrtime()` 返回的结果，用于与当次调用做差值计算。
如果此参数传入的不是一个元数组，则会抛出 `TypeError`。
给此参数传入一个用户定义的数组，而不是传入上次调用 `process.hrtime()` 的结果，则会导致未定义的行为。

返回的时间都是相对于过去某一时刻的值，与一天中的时钟时间没有关系，因此不受制于时钟偏差。
此方法最主要的作用是衡量间隔操作的性能：

```js
const NS_PER_SEC = 1e9;
const time = process.hrtime();
// [ 1800216, 25 ]

setTimeout(() => {
  const diff = process.hrtime(time);
  // [ 1, 552 ]

  console.log(`基准工具 ${diff[0] * NS_PER_SEC + diff[1]} 纳秒`);
  // 基准工具 1000000552 纳秒
}, 1000);
```


