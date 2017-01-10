<!-- YAML
added: v0.3.6
-->

Like [`http.get()`][] but for HTTPS.

`options` can be an object or a string. If `options` is a string, it is
automatically parsed with [`url.parse()`][].

Example:

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

