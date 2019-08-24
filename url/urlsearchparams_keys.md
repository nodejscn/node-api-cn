
* 返回: {Iterator}

在每一个键值对上返回一个键的 ES6 `Iterator`。

```js
const params = new URLSearchParams('foo=bar&foo=baz');
for (const name of params.keys()) {
  console.log(name);
}
// 打印:
//   foo
//   foo
```

