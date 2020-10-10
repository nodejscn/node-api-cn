
* {string}

获取及设置 URL 的主机部分。

```js
const myURL = new URL('https://example.org:81/foo');
console.log(myURL.host);
  // 打印 example.org:81

myURL.host = 'example.com:82';
console.log(myURL.href);
  // 打印 https://example.com:82/foo
```

分配给 `host` 属性的无效主机值将会被忽略。

