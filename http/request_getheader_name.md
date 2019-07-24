<!-- YAML
added: v1.6.0
-->

* `name` {string}
* 返回: {any}

读取请求中的一个请求头。 
注意，该名称不区分大小写。 
返回值的类型取决于提供给 [`request.setHeader()`] 的参数。

```js
request.setHeader('content-type', 'text/html');
request.setHeader('Content-Length', Buffer.byteLength(body));
request.setHeader('Cookie', ['type=ninja', 'language=javascript']);
const contentType = request.getHeader('Content-Type');
// contentType 是 'text/html'。
const contentLength = request.getHeader('Content-Length');
// contentLength 的类型为数值。
const cookie = request.getHeader('Cookie');
// cookie 的类型为字符串数组。
```

