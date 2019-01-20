<!-- YAML
added: v0.4.0
-->

* `name` {string}
* 返回: {any}

读出已排队但未发送到客户端的响应头。 
请注意，该名称不区分大小写。 
返回值的类型取决于提供给 [`response.setHeader()`] 的参数。

```js
response.setHeader('Content-Type', 'text/html');
response.setHeader('Content-Length', Buffer.byteLength(body));
response.setHeader('Set-Cookie', ['type=ninja', 'language=javascript']);
const contentType = response.getHeader('content-type');
// contentType 是 'text/html'。
const contentLength = response.getHeader('Content-Length');
// contentLength 的类型为数值。
const setCookie = response.getHeader('set-cookie');
// setCookie 的类型为字符串数组。
```

