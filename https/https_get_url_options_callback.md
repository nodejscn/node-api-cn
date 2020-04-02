<!-- YAML
added: v0.3.6
changes:
  - version: v10.9.0
    pr-url: https://github.com/nodejs/node/pull/21616
    description: 现在可以将 `url` 参数与一个单独的 `options` 对象一起传入。
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10638
    description: 参数 `options` 可以是 WHATWG `URL` 对象。
-->
* `url` {string | URL}
* `options` {Object | string | URL} 接受与 [`https.request()`] 相同的 `options`, `method` 始终设置为 `GET`。
* `callback` {Function}

类似 [`http.get()`]，但是用于 HTTPS。

`options` 可以是对象、字符串、或 [`URL`] 对象。
如果 `options` 是一个字符串, 则会被自动地使用 [`new URL()`] 解析。
如果是一个 [`URL`] 对象，则会被自动地转换为一个普通的 `options` 对象。

```js
const https = require('https');

https.get('https://encrypted.google.com/', (res) => {
  console.log('状态码:', res.statusCode);
  console.log('请求头:', res.headers);

  res.on('data', (d) => {
    process.stdout.write(d);
  });

}).on('error', (e) => {
  console.error(e);
});
```

