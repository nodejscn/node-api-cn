
* {string}

获取及设置URL的序列化查询(query)部分部分。

```js
const { URL } = require('url');
const myURL = new URL('https://example.org/abc?123');
console.log(myURL.search);
  // 输出 ?123

myURL.search = 'abc=xyz';
console.log(myURL.href);
  // 输出 https://example.org/abc?abc=xyz
```

任何出现在赋给`search`属性值中的无效URL字符将被[百分比编码][]。请注意选择哪些字符进行百分比编码可能与[`url.parse()`][]和[`url.format()`][]方法产生的不同。

