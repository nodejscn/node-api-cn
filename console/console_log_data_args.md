<!-- YAML
added: v0.1.100
-->

打印到 `stdout`，并带上换行符。
可以传入多个参数，第一个参数作为主要信息，其他参数作为类似于 printf(3) 中的代替值（参数都会传给 [`util.format()`]）。

```js
const count = 5;
console.log('count: %d', count);
// 打印: count: 5 到 stdout
console.log('count:', count);
// 打印: count: 5 到 stdout
```

如果在第一个字符串中没有找到格式化元素（如 `%d`），则在每个参数上调用 [`util.inspect()`] 并将结果字符串值拼在一起。
详见 [`util.format()`]。

