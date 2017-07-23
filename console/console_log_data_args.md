<!-- YAML
added: v0.1.100
-->
* `data` {any}
* `...args` {any}

打印到 `stdout`，并带上换行符。
可以传入多个参数，第一个参数作为主要信息，其他参数作为类似于 printf(3) 中的代替值（参数都会传给 [`util.format()`]）。

```js
const count = 5;
console.log('count: %d', count);
// 打印: count: 5 到 stdout
console.log('count:', count);
// 打印: count: 5 到 stdout
```

详见 [`util.format()`]。

