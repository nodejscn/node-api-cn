
* {string}

获取及设置URL的用户名(username)部分。

```js
const { URL } = require('url');
const myURL = new URL('https://abc:xyz@example.com');
console.log(myURL.username);
  // 输出 abc

myURL.username = '123';
console.log(myURL.href);
  // 输出 https://123:xyz@example.com/
```

任何出现在赋给`username`属性值中的无效URL字符将被[百分比编码][]。请注意选择哪些字符进行百分比编码可能与[`url.parse()`][]和[`url.format()`][]方法产生的不同。

