
* {string}

获取并设置URL的username部分。

```js
const { URL } = require('url');
const myURL = new URL('https://abc:xyz@example.com');
console.log(myURL.username);
  // 输出 abc

myURL.username = '123';
console.log(myURL.href);
  // 输出 https://123:xyz@example.com/
```
任何无效URL出现在`username`属性值的字符将会是[百分比编码][]。请注意选择哪些字符到百分比编码可能与[`url.parse()`][]和[`url.format()`][]方法产生的不同。
