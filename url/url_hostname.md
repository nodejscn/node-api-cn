
* {string}

获取及设置 URL 的主机名部分。 
`url.host` 和 `url.hostname` 之间的区别是 `url.hostname` 不包含端口。

```js
const myURL = new URL('https://example.org:81/foo');
console.log(myURL.hostname);
  // 打印 example.org

myURL.hostname = 'example.com:82';
console.log(myURL.href);
  // 打印 https://example.com:81/foo
```

为 `hostname` 属性设置无效的值则会被忽略。

