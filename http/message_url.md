<!-- YAML
added: v0.1.90
-->

* {string}

**仅在 [`http.Server`] 返回的请求中有效。**

返回请求的 URL 字符串。
仅包含实际 HTTP 请求中的 URL。
如果请求是：


```txt
GET /status?name=ryan HTTP/1.1\r\n
Accept: text/plain\r\n
\r\n
```

则 `request.url` 会是：

<!-- eslint-disable semi -->
```js
'/status?name=ryan'
```

如果想将 url 解析成各个部分，可以使用 `require('url').parse(request.url)`。
例子：

```txt
$ node
> require('url').parse('/status?name=ryan')
Url {
  protocol: null,
  slashes: null,
  auth: null,
  host: null,
  port: null,
  hostname: null,
  hash: null,
  search: '?name=ryan',
  query: 'name=ryan',
  pathname: '/status',
  path: '/status?name=ryan',
  href: '/status?name=ryan' }
```

如果想从查询字符串中提取参数，可以使用 `require('querystring').parse` 函数、或为 `require('url').parse` 的第二个参数传入 `true`。
例子：

```txt
$ node
> require('url').parse('/status?name=ryan', true)
Url {
  protocol: null,
  slashes: null,
  auth: null,
  host: null,
  port: null,
  hostname: null,
  hash: null,
  search: '?name=ryan',
  query: { name: 'ryan' },
  pathname: '/status',
  path: '/status?name=ryan',
  href: '/status?name=ryan' }
```

