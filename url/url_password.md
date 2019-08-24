
* {string}

获取及设置 URL 的密码部分。

```js
const myURL = new URL('https://abc:xyz@example.com');
console.log(myURL.password);
  // 打印 xyz

myURL.password = '123';
console.log(myURL.href);
  // 打印 https://abc:123@example.com
```

分配给 `password` 属性的值中包含的无效 URL 字符是[百分比编码的][percent-encoded]。 
选择哪些字符进行百分比编码可能与 [`url.parse()`] 和 [`url.format()`] 方法产生的内容有所不同。


