<!-- YAML
added: v0.1.90
-->

* {String}

**Only valid for request obtained from [`http.Server`][].**

Request URL string. This contains only the URL that is
present in the actual HTTP request. If the request is:

```txt
GET /status?name=ryan HTTP/1.1\r\n
Accept: text/plain\r\n
\r\n
```

Then `request.url` will be:

```js
'/status?name=ryan'
```

If you would like to parse the URL into its parts, you can use
`require('url').parse(request.url)`.  Example:

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

If you would like to extract the parameters from the query string,
you can use the `require('querystring').parse` function, or pass
`true` as the second argument to `require('url').parse`.  Example:

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

