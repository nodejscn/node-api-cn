
* {string}

获取及设置 URL 的片段部分。

```js
const myURL = new URL('https://example.org/foo#bar');
console.log(myURL.hash);
  // 打印 #bar

myURL.hash = 'baz';
console.log(myURL.href);
  // 打印 https://example.org/foo#baz
```

分配给 `hash` 属性的值中包含的无效 URL 字符是[百分比编码的][percent-encoded]。 
选择哪些字符进行百分比编码可能与 [`url.parse()`] 和 [`url.format()`] 方法产生的内容有所不同。

