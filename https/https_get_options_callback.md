<!-- YAML
added: v0.3.6
-->

类似[`http.get()`][]，但是却是用于HTTPS的.

参数`options` 可以是一个对象或是一个字符串. 如果参数`options` 是一个字符串, 它自动被[`url.parse()`][]所解析.

例子:

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

