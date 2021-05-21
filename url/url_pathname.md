
* {string}

获取和设置 URL 的路径部分。

```js
const myURL = new URL('https://example.org/abc/xyz?123');
console.log(myURL.pathname);
  // 打印 /abc/xyz

myURL.pathname = '/abcdef';
console.log(myURL.href);
  // 打印 https://example.org/abcdef?123
```

被分配给 `pathname` 属性的值中所包含的无效的 URL 字符会被[百分比编码][percent-encoded]。 
对哪些字符要百分比编码的选择可能与 [`url.parse()`] 和 [`url.format()`] 方法产生的内容有所不同。


