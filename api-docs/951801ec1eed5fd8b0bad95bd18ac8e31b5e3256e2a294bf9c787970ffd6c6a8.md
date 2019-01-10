
* {string}

获取及设置URL的路径(path)部分。

```js
const { URL } = require('url');
const myURL = new URL('https://example.org/abc/xyz?123');
console.log(myURL.pathname);
  // 输出 /abc/xyz

myURL.pathname = '/abcdef';
console.log(myURL.href);
  // 输出 https://example.org/abcdef?123
```

包含在赋给`pathname`属性的值中的无效URL字符是[百分比编码][]。请注意选择哪些字符进行百分比编码可能与[`url.parse()`][]和[`url.format()`][]方法产生的不同。

