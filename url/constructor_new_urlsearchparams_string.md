
* `string` {string} 一个查询字符串

将`string`解析成一个查询字符串, 并且使用它来实例化一个新的`URLSearchParams`对象.  如果`string`以`'?'`打头,则`'?'`将会被忽略.

```js
const { URLSearchParams } = require('url');
let params;

params = new URLSearchParams('user=abc&query=xyz');
console.log(params.get('user'));
  // 输出 'abc'
console.log(params.toString());
  // 输出 'user=abc&query=xyz'

params = new URLSearchParams('?user=abc&query=xyz');
console.log(params.toString());
  // 输出 'user=abc&query=xyz'
```

