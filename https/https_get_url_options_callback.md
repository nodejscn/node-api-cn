<!-- YAML
added: v0.3.6
changes:
  - version: v10.9.0
    pr-url: https://github.com/nodejs/node/pull/21616
    description: allow both url and options to be passed to `https.get()`
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10638
    description: The `options` parameter can be a WHATWG `URL` object.
-->
* `url` {string | URL}
* `options` {Object | string | URL} Accepts the same `options` as
  [`https.request()`][], with the `method` always set to `GET`.
* `callback` {Function}

Like [`http.get()`][] but for HTTPS.

`options` can be an object, a string, or a [`URL`][] object. If `options` is a
string, it is automatically parsed with [`url.parse()`][]. If it is a [`URL`][]
object, it will be automatically converted to an ordinary `options` object.

```js
const https = require('https');

https.get('https://encrypted.google.com/', (res) => {
  console.log('statusCode:', res.statusCode);
  console.log('headers:', res.headers);

  res.on('data', (d) => {
    process.stdout.write(d);
  });

}).on('error', (e) => {
  console.error(e);
});
```

