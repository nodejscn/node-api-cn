
* {string}

获取及设置URL的密码(password)部分。

```js
const { URL } = require('url');
const myURL = new URL('https://abc:xyz@example.com');
console.log(myURL.password);
  // 输出 xyz

myURL.password = '123';
console.log(myURL.href);
  // 输出 https://abc:123@example.com
```

包含在赋给`password`属性的值中的无效URL字符是[百分比编码][]。请注意选择哪些字符进行百分比编码可能与[`url.parse()`][]和[`url.format()`][]方法产生的不同。

