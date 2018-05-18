
* Returns: {Iterator}

根据查询字符串，返回一个键值对形式的 ES6 `Iterator`。每个迭代器的项是一个 JavaScript `Array`。
其中，`Array` 的第一项是 `name`，第二个是 `value`。

是 [`urlSearchParams.entries()`][] 的别名。

```js
const params = new URLSearchParams('foo=bar&xyz=baz');
for (const [name, value] of params) {
  console.log(name, value);
}
// Prints:
//   foo bar
//   xyz baz
```

