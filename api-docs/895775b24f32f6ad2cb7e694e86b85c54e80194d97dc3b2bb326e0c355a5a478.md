<!-- YAML
added: v0.4.0
-->

* `name` {string}
* 返回: {any}

读取一个已入队列但尚未发送到客户端的响应头。
名称不区分大小写。
返回值的类型取决于传入 [`response.setHeader()`] 的参数。

```js
response.setHeader('Content-Type', 'text/html');
response.setHeader('Content-Length', Buffer.byteLength(body));
response.setHeader('Set-Cookie', ['type=ninja', 'language=javascript']);
const contentType = response.getHeader('content-type');
// contentType 的值为 'text/html'。
const contentLength = response.getHeader('Content-Length');
// contentLength 是一个数值。
const setCookie = response.getHeader('set-cookie');
// setCookie 是一个字符串数组。
```

