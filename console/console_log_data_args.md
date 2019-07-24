<!-- YAML
added: v0.1.100
-->
* `data` {any}
* `...args` {any}

打印到 `stdout`，并加上换行符。
可以传入多个参数，第一个参数作为主要信息，其他参数作为类似于 printf(3) 中的代替值（参数都会传给 [`util.format()`]）。

```js
const count = 5;
console.log('计数: %d', count);
// 打印到 stdout: 计数: 5 
console.log('计数:', count);
// 打印到 stdout: 计数: 5 
```

有关更多信息，请参见 [`util.format()`]。

