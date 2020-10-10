
* {string}

获取及设置 URL 的路径部分。

```js
const myURL = new URL('https://example.org/abc/xyz?123');
console.log(myURL.pathname);
  // 打印 /abc/xyz

myURL.pathname = '/abcdef';
console.log(myURL.href);
  // 打印 https://example.org/abcdef?123
```

分配给 `pathname` 属性的值中包含的无效 URL 字符是[百分比编码的][percent-encoded]。 
选择哪些字符进行百分比编码可能与 [`url.parse()`] 和 [`url.format()`] 方法产生的内容有所不同。


