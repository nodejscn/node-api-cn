
* {string}

获取及设置URL的分段(hash)部分。

```js
const { URL } = require('url');
const myURL = new URL('https://example.org/foo#bar');
console.log(myURL.hash);
  // 输出 #bar

myURL.hash = 'baz';
console.log(myURL.href);
  // 输出 https://example.org/foo#baz
```

包含在赋给`hash`属性的值中的无效URL字符是[百分比编码][]。请注意选择哪些字符进行百分比编码可能与[url.parse()][]和[url.format()][]方法产生的不同。

