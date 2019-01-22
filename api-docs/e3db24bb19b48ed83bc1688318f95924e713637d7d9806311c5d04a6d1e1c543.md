<!-- YAML
added: v0.1.90
-->

* {string}

仅对从 [`http.Server`] 获取的请求有效。

请求的 URL 字符串。
它仅包含实际 HTTP 请求中存在的 URL。
如果请求是：

```txt
GET /status?name=ryan HTTP/1.1\r\n
Accept: text/plain\r\n
\r\n
```

则 `request.url` 将是：

<!-- eslint-disable semi -->
```js
'/status?name=ryan'
```

要将 url 解析为其各个部分，可以使用 `require('url').parse(request.url)`：

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

要从查询字符串中提取参数，可以使用 `require('querystring').parse` 函数，或者可以将 `true` 作为第二个参数传递给 `require('url').parse`：

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

