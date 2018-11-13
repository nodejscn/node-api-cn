<!-- YAML
added: v1.6.0
-->

* `name` {string}
* Returns: {any}

读取请求头。
请求头的键名是大小写不敏感的。

返回值得类型取决于传入 [`request.setHeader()`] 的参数。
例子：

```js
request.setHeader('content-type', 'text/html');
request.setHeader('Content-Length', Buffer.byteLength(body));
request.setHeader('Set-Cookie', ['type=ninja', 'language=javascript']);
const contentType = request.getHeader('Content-Type');
// contentType 的值为 'text/html'。
const contentLength = request.getHeader('Content-Length');
// contentLength 是一个数值。
const setCookie = request.getHeader('set-cookie');
// setCookie 是一个字符串数组。
```

