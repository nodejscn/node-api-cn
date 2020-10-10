<!-- YAML
added: v0.1.100
-->
* `data` {any}
* `...args` {any}

用换行符打印到 `stderr`。
可以传入多个参数，第一个参数用作主要信息，所有其他参数用作类似于 printf(3) 中的替换值（参数都传给 [`util.format()`]）。

```js
const code = 5;
console.error('error #%d', code);
// 打印到 stderr: error #5
console.error('error', code);
// 打印到 stderr: error 5
```

如果在第一个字符串中找不到格式化元素（例如 `％d`），则会在每个参数上调用 [`util.inspect()`]，并且连接结果字符串值。 
有关更多信息，请参见 [`util.format()`]。

