
* `string` {string} 查询字符串。

将 `string` 解析成一个查询字符串, 并且使用它来实例化一个新的 `URLSearchParams` 对象。
如果以 `'?'` 开头，则忽略.

```js
let params;

params = new URLSearchParams('user=abc&query=xyz');
console.log(params.get('user'));
// 打印 'abc'
console.log(params.toString());
// 打印 'user=abc&query=xyz'

params = new URLSearchParams('?user=abc&query=xyz');
console.log(params.toString());
// 打印 'user=abc&query=xyz'
```

