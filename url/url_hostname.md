
* {string}

获取及设置 URL 的主机名部分。 
`url.host` 和 `url.hostname` 之间的区别是 `url.hostname` 不包含端口。

```js
const myURL = new URL('https://example.org:81/foo');
console.log(myURL.hostname);
// 打印 example.org

// 设置 hostname 不会更改端口。
myURL.hostname = 'example.com:82';
console.log(myURL.href);
// 打印 https://example.com:81/foo
  
// 使用 host 会更改主机名和端口。
myURL.host = 'example.org:82';
console.log(myURL.href);
// 打印 https://example.org:82/foo
```

为 `hostname` 属性设置无效的值则会被忽略。

