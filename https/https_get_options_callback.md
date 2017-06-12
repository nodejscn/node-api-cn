<!-- YAML
added: v0.3.6
changes:
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10638
    description: The `options` parameter can be a WHATWG `URL` object.
-->
- `options` {Object | string | URL} Accepts the same `options` as
  [`https.request()`][], with the `method` always set to `GET`.
- `callback` {Function}

类似 [`http.get()`]，但是用于 HTTPS。

参数 `options` 可以是一个对象、或字符串、或 [`URL`] 对象。
如果参数 `options` 是一个字符串, 它自动被 [`url.parse()`] 所解析。
If it is a [`URL`][] object, it will be automatically converted to an ordinary `options` object.

例子:

```js
const https = require('https');

https.get('https://encrypted.google.com/', (res) => {
  console.log('状态码：', res.statusCode);
  console.log('请求头：', res.headers);

  res.on('data', (d) => {
    process.stdout.write(d);
  });

}).on('error', (e) => {
  console.error(e);
});
```

