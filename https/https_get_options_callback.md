<!-- YAML
added: v0.3.6
-->

类似 [`http.get()`]，但是用于 HTTPS。

参数 `options` 可以是一个对象或是一个字符串。
如果参数 `options` 是一个字符串, 它自动被 [`url.parse()`] 所解析。

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

