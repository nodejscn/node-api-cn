
* {string}

获取及设置 URL 的协议部分。

```js
const myURL = new URL('https://example.org');
console.log(myURL.protocol);
// 打印 https:

myURL.protocol = 'ftp';
console.log(myURL.href);
// 打印 ftp://example.org/
```

分配给 `protocol` 属性的无效协议值将会被忽略。

