<!-- YAML
added: v0.1.90
-->

* {String}

**仅适用于从 [`http.Server`] 获得的请求。**

请求的 URL 字符串。
仅包含 HTTP 请求实际存在的 URL。
如果请求是：


```txt
GET /status?name=ryan HTTP/1.1\r\n
Accept: text/plain\r\n
\r\n
```

则 `request.url` 会是：

```js
'/status?name=ryan'
```

如果想将 URL 解析成各个部分，可以使用 `require('url').parse(request.url)`。
例子：

```txt
$ node
> require('url').parse('/status?name=ryan')
{
  href: '/status?name=ryan',
  search: '?name=ryan',
  query: 'name=ryan',
  pathname: '/status'
}
```

如果想从查询字符串中提取参数，可以使用 `require('querystring').parse` 函数，或传入 `true` 作为 `require('url').parse` 的第二个参数。
例子：

```txt
$ node
> require('url').parse('/status?name=ryan', true)
{
  href: '/status?name=ryan',
  search: '?name=ryan',
  query: {name: 'ryan'},
  pathname: '/status'
}
```

