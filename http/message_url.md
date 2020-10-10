<!-- YAML
added: v0.1.90
-->

* {string}

仅对从 [`http.Server`] 获取的请求有效。

请求的 URL 字符串。
它仅包含实际的 HTTP 请求中存在的 URL。
以下面的请求为例：

```http
GET /status?name=ryan HTTP/1.1
Accept: text/plain
```

要将 URL 解析成各个部分：

```js
new URL(request.url, `http://${request.headers.host}`);
```

当 `request.url` 是 `'/status?name=ryan'` 且 `request.headers.host` 是 `'localhost:3000'` 时：

```console
$ node
> new URL(request.url, `http://${request.headers.host}`)
URL {
  href: 'http://localhost:3000/status?name=ryan',
  origin: 'http://localhost:3000',
  protocol: 'http:',
  username: '',
  password: '',
  host: 'localhost:3000',
  hostname: 'localhost',
  port: '3000',
  pathname: '/status',
  search: '?name=ryan',
  searchParams: URLSearchParams { 'name' => 'ryan' },
  hash: ''
}
```

